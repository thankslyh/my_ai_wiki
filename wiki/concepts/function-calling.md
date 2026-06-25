---
title: Function Calling（工具调用原理）
type: concept
created: 2026-06-25
tags: [concept]
---

# Function Calling（工具调用原理）

> 大模型「调用工具」的底层机制：模型只生成文本，真正的执行由外部程序完成。

## 是什么

Claude 本身只会生成文本，从不真正执行工具。所谓 tool use（function calling）是一个**模型负责决策、外部程序负责执行**的协作循环：模型输出结构化的「我想调用某工具 + 参数」→ 外部程序（harness）解析并真正执行 → 结果塞回对话 → 模型继续推理。来源：[[ai-agent-from-tools-to-concurrency]]。

## 关键点

- **工具定义三要素**：`name`、`description`（极其重要，模型靠它判断何时怎么用）、`input_schema`（JSON Schema 约束参数结构）。
- **关键消息块**：模型产出 `tool_use`（含 `id`/`name`/`input`），外部回传 `tool_result`（`tool_use_id` 必须一一对上）。
- API 层用约束解码保证参数是合法 JSON；一次回复可含多个 `tool_use` 实现并行调用。
- 它是构建 [[ai-agent-loop]] 的最小积木：循环地「请求模型 → 执行工具 → 回传结果」直到模型不再要求调用工具。

## 易踩坑（来自最小 Agent Loop 实现）

- `assistant` 回复必须**原样 push** 回 messages（含 tool_use block），否则 id 对不上报错。
- `tool_result` 的 role 是 **`user`**，不是 "tool"。
- 退出判据是 `stop_reason !== "tool_use"`，别用「有没有文字」判断。
- 并行工具：一次可能多个 tool_use，全跑完后**合并成一条** user 消息回传。

## 相关

- [[ai-agent-loop]] —— 用 function calling 搭起来的最小循环
- [[claude-code-mcp]] —— MCP 是工具接入的标准化协议
- 来源：[[ai-agent-from-tools-to-concurrency]]
