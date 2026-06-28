---
title: "AI Agent 原理笔记：从 Tool 到多 Agent 并发控制"
source: 与 Claude 的对话沉淀
source_url: 待补充（对话沉淀，无外部 URL）
created: 2026-06-25
tags: [clip]
---


# AI Agent 原理笔记：从 Tool 到多 Agent 并发控制

## summary
本文沉淀一次系统性对话，从最底层的 Tool（function calling）原理出发，逐层向上推进：Tool 的本质是「模型决策 + 外部程序执行」的协作循环 → 最小 Agent Loop 的实现与退出条件 → 「AI Agent ≈ 操作系统」的同构类比 → 多 Agent 协作的拓扑与价值 → Agent 间通信（IPC）的设计 → 共享黑板并发写的加锁与版本控制。贯穿全文的核心直觉是：**Agent 的功夫本质是「上下文工程 + 分布式系统设计」，只不过把确定性内核换成了概率性模型**。

## key_points

### 1. Tool 的本质
- Claude 本身**只会生成文本**，从不真正执行工具。所谓 tool use 是：模型输出结构化的「我想调用某工具+参数」→ 外部程序（harness）解析并真正执行 → 结果塞回对话 → 模型继续推理。
- 这是一个**模型负责决策、外部程序负责执行**的协作循环。
- 工具定义三要素：`name`、`description`（极其重要，模型靠它判断何时怎么用）、`input_schema`（JSON Schema 约束参数结构）。
- 关键消息块：模型产出 `tool_use`（含 `id`/`name`/`input`），外部回传 `tool_result`（`tool_use_id` 必须对上）。
- API 层用约束解码保证参数合法 JSON；一次回复可含多个 `tool_use` 实现并行调用。

### 2. 最小 Agent Loop（TS）
循环骨架：
```
user 提问
  └→ while:
       请求模型
       存 assistant 输出（必须原样 push，含 tool_use block）
       if stop_reason !== "tool_use" → 打印答案 break
       else → 执行所有工具 → 合并成一条 tool_result(user) 回传 → 继续
```
五个易踩坑：
1. `assistant` 回复必须**原样 push** 回 messages（含 tool_use block），否则 id 对不上报错。
2. `tool_result` 的 role 是 **`user`**，不是 "tool"。
3. `tool_use_id` 必须精确一一对应。
4. 退出判据是 `stop_reason !== "tool_use"`，别用「有没有文字」判断。
5. 并行工具：一次可能多个 tool_use，全跑完后**合并成一条** user 消息回传。

### 3. while(true) 的退出条件
- **正常出口**：看 `stop_reason`。`tool_use`=继续；`end_turn`=正常收尾退出；`max_tokens`=被截断退出（答案不完整）；`stop_sequence`=退出；`pause_turn`=原样回传继续。
- **安全护栏（生产必加）**：①最大轮次限制（防工具无限循环，最重要）；②token/成本预算；③超时。
- **异常出口**：工具不存在 → 回传 `is_error:true` 让模型纠正；API 报错 → try-catch 重试；用户中断（Esc）→ 外部强行 break。
- 一句话：**正常退出靠模型的 stop_reason，安全退出靠自己加的轮次/预算/超时护栏**。

### 4. AI Agent ≈ 操作系统（同构异核）
对应关系：CPU↔LLM、进程/线程↔任务/subagent、syscall↔tool call、内存RAM↔上下文窗口、硬盘↔外部记忆/向量库、驱动driver↔MCP/工具适配器、内核kernel↔agent loop、Shell↔自然语言 prompt、权限沙箱↔tool 权限审批。
- 最深刻的类比是 **syscall ↔ tool call**：受限的大脑通过特权接口触碰外部世界。
- **context = 新的内存管理难题**：context 满≈内存溢出（需压缩/摘要，像换页 swap）；长期记忆≈存硬盘；prompt 缓存≈CPU cache。「上下文工程」约等于 OS 的「内存管理」。
- **agent loop = kernel 调度器**。
- 类比的边界：OS 是**确定性**、可形式化验证；Agent 是**概率性**、会幻觉、软调度、需大量护栏。准确说法是「**架构同构、内核异质**」。
- 业界趋势 "LLM as OS"（Karpathy）：LLM 是新 CPU，context 是内存，工具是外设，自然语言是新 shell。

### 5. 多 Agent 协作
- 单 Agent 三堵墙：context 爆、注意力涣散、无法并行。
- 类比多进程/分布式：Orchestrator↔主进程调度器、subagent↔worker、独立 context↔独立内存空间、消息传递↔IPC、spawn↔fork、汇总↔join、fan-out/fan-in↔Map-Reduce。
- 四种拓扑：①**Orchestrator-Worker**（主管-工人，最常用）；②**Pipeline**（流水线，像 Unix 管道）；③**Debate/Voting**（辩论投票，对抗幻觉）；④**Generator-Critic**（生成-批评反思）。
- **最大价值是 context 隔离**（不是更聪明）：每个 subagent 独立干净上下文，主 Agent 只拿压缩后的结论，变相扩展系统总有效上下文。
- 老大难（=分布式老坑）：通信成本高、状态不一致、协调开销、错误传播（级联失败）、死锁空转、结果难合并。
- 判断标准：子任务**独立可并行/需多视角/单任务 context 会爆/有清晰工序** → 上多 Agent；**简单任务/强依赖串行/只为显得高级** → 别上。本质是「用协调成本换并行+隔离+多视角」。

### 6. Agent 间通信（IPC）设计
- 核心矛盾：传的不是内存指针而是自然语言/结构化数据，**每个字都花 token** → 信息要传够 vs 别传太多。
- 四种模式：①**直接传参**（≈管道，Orchestrator-Worker 用，星形）；②**共享黑板**（≈共享内存，文件/DB/KV，要处理并发写）；③**消息队列**（≈MQ，异步解耦、广播扇出）；④**编排器中转**（≈中心路由，控制力强但单点瓶颈）。
- **Payload 设计才是精髓**（区别于传统 IPC）：
  1. subagent 返回前先**压缩**（传结论不传过程）。
  2. 用**结构化 schema** 而非自由文本（定义 IPC 协议格式）。
  3. **need-to-know**：只传下游干活需要的，省 token 防带偏。
- 神技：**传引用而非实体**（大数据写文件，IPC 只传路径），对应 OS 传内存地址而非拷贝整块内存。

### 7. 共享黑板并发写：加锁与版本控制
问题本质 = 经典 **Lost Update（更新丢失）**：两个 Agent 各读旧版本，后写覆盖先写。
- **悲观锁**（先抢锁再写）：用文件原子创建（`flag:'wx'`）当锁。简单不丢更新，但 **Agent 操作以秒计，持锁久 → 并行度暴跌**，还有死锁/锁泄漏风险。**对 Agent 不友好，下策**。
- **乐观锁 + CAS**（⭐ Agent 场景最佳锁方案）：数据带版本号，提交时 Compare-And-Swap 校验版本没变才写入并 +1，冲突则重读重试（退避）。不阻塞、并行度高、无死锁，适合「冲突其实不频繁」的 Agent 场景。
- **从源头避免争抢**（更高明）：
  1. **分区写 Sharding**（最实用）：各 Agent 写各自文件（A.json/B.json），Orchestrator 最后合并 → 零冲突。
  2. **Append-only 事件日志**：只追加不改，最终态由重放算出（Event Sourcing）。
  3. **CRDT**：数学保证合并一致的数据结构，重武器，一般用不到。
- 两个必加护栏：①**锁/操作超时**（Agent 崩了锁也自动失效，防卡死全场；时间戳从外部传入避免不确定性）；②**写入 schema 校验**（Agent 会幻觉，脏数据比丢数据更致命）。
- 核心直觉：**Agent 操作以秒计且会幻觉，越「无锁、越分区、越异步」的设计越适合它**。

## 决策表速查

并发控制选型：
- Agent 各干各的、结果独立 → **分区写**（首选，零冲突）
- 只增不改、要审计 → **Append-only 日志**
- 必须共改、冲突少 → **乐观锁 + CAS**（Agent 最佳）
- 必须共改、冲突频繁且改动重 → **悲观锁 + 超时**（慎用）
- 强一致性要求极高 → **CRDT / 事务**

IPC 模式选型：
- 主管派活一问一答 → 直接传参
- 多 Agent 长期协作共享状态 → 共享黑板
- 大规模松耦合异步 → 消息队列
- 需强管控权限过滤 → 编排器中转
- 数据量大 → 任何模式 + 传引用不传实体

## related_concepts
- [[function-calling]] —— Tool 调用底层原理（第 1 节）
- [[ai-agent-loop]] —— 最小智能体循环与退出条件（第 2-3 节）
- [[llm-as-os]] —— AI Agent ≈ 操作系统（第 4 节）
- [[multi-agent-collaboration]] —— 多 Agent 协作与 IPC（第 5-6 节）
- [[agent-concurrency-control]] —— 共享黑板并发写控制（第 7 节）
- [[context-engineering]] —— 上下文工程（贯穿全文）
- [[claude-code]] · [[claude-code-subagents]] · [[claude-code-mcp]] —— Claude Code 中的对应实现
