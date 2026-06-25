---
title: Context Engineering（上下文工程）
type: concept
created: 2026-06-25
tags: [concept]
---

# Context Engineering（上下文工程）

> 管理有限上下文窗口这一稀缺资源的工程实践，类比操作系统的「内存管理」。

## 是什么

上下文工程是围绕「有限的上下文窗口」做资源管理的工程实践。在 [[llm-as-os]] 的类比里，context 就是内存，于是上下文工程约等于 OS 的内存管理：什么放进窗口、什么压缩摘要、什么换出到外部存储。它是 AI Agent 功夫的核心之一——「Agent 的功夫本质是上下文工程 + 分布式系统设计」。来源：[[ai-agent-from-tools-to-concurrency]]。

## 关键点

- **context 满 ≈ 内存溢出**：需要压缩 / 摘要，类比换页 swap。
- **长期记忆 ≈ 存硬盘**：超出窗口的内容沉淀到外部记忆 / 向量库。
- **prompt 缓存 ≈ CPU cache**：复用稳定前缀降低成本与延迟。
- **多 Agent 的最大价值是 context 隔离**：每个 subagent 独立干净上下文，主 Agent 只拿压缩后的结论，变相扩展系统总有效上下文 → 见 [[claude-code-subagents]]。
- **IPC 的 Payload 设计也是上下文工程**：subagent 返回前先压缩（传结论不传过程）、用结构化 schema、need-to-know 只传必要信息、大数据传引用不传实体。

## 相关

- [[llm-as-os]] —— 上下文工程对应其中的内存管理
- [[claude-code-subagents]] —— context 隔离是多 Agent 的核心价值
- [[claude-code-memory]] —— 跨会话的外部记忆
- 来源：[[ai-agent-from-tools-to-concurrency]]
