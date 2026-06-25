---
title: AI Agent Loop（最小智能体循环）
type: concept
created: 2026-06-25
tags: [concept]
---

# AI Agent Loop（最小智能体循环）

> Agent 的内核：循环地「请求模型 → 执行工具 → 回传结果」，直到模型不再要求调用工具。对应 [[llm-as-os]] 里的 kernel 调度器。

## 是什么

Agent Loop 是把 [[function-calling]] 串成自治循环的最小骨架。用户提问后进入 while 循环：请求模型 → 存下 assistant 输出 → 若不再要求调用工具则收尾退出，否则执行所有工具、合并结果回传、继续。来源：[[ai-agent-from-tools-to-concurrency]]。

```
user 提问
  └→ while:
       请求模型
       存 assistant 输出（必须原样 push，含 tool_use block）
       if stop_reason !== "tool_use" → 打印答案 break
       else → 执行所有工具 → 合并成一条 tool_result(user) 回传 → 继续
```

## 退出条件

- **正常出口靠 `stop_reason`**：`tool_use`=继续；`end_turn`=正常收尾；`max_tokens`=被截断（答案不完整）；`stop_sequence`=退出；`pause_turn`=原样回传继续。
- **安全护栏（生产必加）**：① 最大轮次限制（防工具无限循环，最重要）；② token / 成本预算；③ 超时。
- **异常出口**：工具不存在 → 回传 `is_error:true` 让模型纠正；API 报错 → try-catch 重试；用户中断（Esc）→ 外部强行 break。
- 一句话：**正常退出靠模型的 stop_reason，安全退出靠自己加的轮次 / 预算 / 超时护栏**。

## 相关

- [[function-calling]] —— 循环里每一步的工具调用机制
- [[llm-as-os]] —— Agent Loop ≈ 内核调度器
- [[multi-agent-collaboration]] —— 多个 Agent Loop 的协作
- 来源：[[ai-agent-from-tools-to-concurrency]]
