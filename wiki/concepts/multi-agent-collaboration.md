---
title: 多 Agent 协作
type: concept
created: 2026-06-25
tags: [concept]
---

# 多 Agent 协作

> 把任务拆给多个 Agent 并行 / 分工，本质是用协调成本换「并行 + 隔离 + 多视角」。类比多进程 / 分布式系统。

## 是什么

单 Agent 有三堵墙：context 爆、注意力涣散、无法并行。多 Agent 协作借用多进程 / 分布式的思路破墙：Orchestrator ↔ 主进程调度器、subagent ↔ worker、独立 context ↔ 独立内存空间、消息传递 ↔ IPC、spawn ↔ fork、汇总 ↔ join、fan-out/fan-in ↔ Map-Reduce。来源：[[ai-agent-from-tools-to-concurrency]]。

## 四种拓扑

1. **Orchestrator-Worker**（主管-工人，最常用）
2. **Pipeline**（流水线，像 Unix 管道）
3. **Debate/Voting**（辩论投票，对抗幻觉）
4. **Generator-Critic**（生成-批评反思）

## 关键点

- **最大价值是 context 隔离**（不是更聪明）：每个 subagent 独立干净上下文，主 Agent 只拿压缩后的结论，变相扩展系统总有效上下文 → 见 [[context-engineering]]。
- **老大难 = 分布式老坑**：通信成本高、状态不一致、协调开销、错误传播（级联失败）、死锁空转、结果难合并。
- **何时该上**：子任务独立可并行 / 需多视角 / 单任务 context 会爆 / 有清晰工序。
- **何时别上**：简单任务 / 强依赖串行 / 只为显得高级。

## Agent 间通信（IPC）

- 核心矛盾：传的不是内存指针而是自然语言 / 结构化数据，**每个字都花 token** → 信息要传够 vs 别传太多。
- 四种模式：① 直接传参（≈管道，星形）；② [[agent-concurrency-control|共享黑板]]（≈共享内存，要处理并发写）；③ 消息队列（≈MQ，异步解耦广播）；④ 编排器中转（≈中心路由，控制强但单点瓶颈）。
- **Payload 设计是精髓**：返回前先压缩（传结论不传过程）、用结构化 schema、need-to-know 只传必要信息。
- 神技：**传引用而非实体**（大数据写文件，IPC 只传路径），对应 OS 传内存地址而非拷贝整块内存。

## 相关

- [[ai-agent-loop]] —— 单个 Agent 的内核
- [[agent-concurrency-control]] —— 共享黑板的并发写控制
- [[claude-code-subagents]] —— Claude Code 的 subagent 实现
- [[context-engineering]] —— context 隔离是核心价值
- 来源：[[ai-agent-from-tools-to-concurrency]]
