---
title: LLM as OS（LLM 即操作系统）
type: concept
created: 2026-06-25
tags: [concept]
---

# LLM as OS（LLM 即操作系统）

> 把 AI Agent 类比成操作系统的思维框架：架构同构，但内核异质（确定性 → 概率性）。

## 是什么

"LLM as OS"（Karpathy 提出的趋势说法）把 AI Agent 与操作系统做同构类比：LLM 是新的 CPU，context 是内存，工具是外设，自然语言是新的 shell。这个框架帮助用成熟的 OS / 分布式系统经验去设计 Agent。来源：[[ai-agent-from-tools-to-concurrency]]。

## 对应关系

| 操作系统 | AI Agent |
| --- | --- |
| CPU | LLM |
| 进程 / 线程 | 任务 / subagent |
| **syscall** | **tool call**（最深刻的类比：受限的大脑通过特权接口触碰外部世界）|
| 内存 RAM | 上下文窗口 |
| 硬盘 | 外部记忆 / 向量库 |
| 驱动 driver | MCP / 工具适配器 |
| 内核 kernel | agent loop |
| Shell | 自然语言 prompt |
| 权限沙箱 | tool 权限审批 |

## 关键点

- **context = 新的内存管理难题**：context 满 ≈ 内存溢出（需压缩 / 摘要，像换页 swap）；长期记忆 ≈ 存硬盘；prompt 缓存 ≈ CPU cache。所谓 [[context-engineering|上下文工程]] 约等于 OS 的「内存管理」。
- **agent loop = kernel 调度器**（见 [[ai-agent-loop]]）。
- **类比的边界**：OS 是确定性、可形式化验证；Agent 是概率性、会幻觉、软调度、需大量护栏。准确说法是「**架构同构、内核异质**」。

## 相关

- [[ai-agent-loop]] —— 对应内核调度器
- [[context-engineering]] —— 对应内存管理
- [[function-calling]] —— 对应 syscall
- 来源：[[ai-agent-from-tools-to-concurrency]]
