---
title: Agent 并发控制
type: concept
created: 2026-06-25
tags: [concept]
---

# Agent 并发控制

> 多个 Agent 共享黑板（文件 / DB）并发写时，如何避免 Lost Update。核心直觉：Agent 操作以秒计且会幻觉，越「无锁、越分区、越异步」越适合它。

## 是什么

当多个 Agent 共享同一份状态（共享黑板）并发写入，会遇到经典的 **Lost Update（更新丢失）**：两个 Agent 各读旧版本，后写覆盖先写。本页整理可选的并发控制方案及其对 Agent 场景的适配度。来源：[[ai-agent-from-tools-to-concurrency]]。

## 各方案对比

- **悲观锁**（先抢锁再写）：用文件原子创建（`flag:'wx'`）当锁。简单不丢更新，但 **Agent 操作以秒计，持锁久 → 并行度暴跌**，还有死锁 / 锁泄漏风险。**对 Agent 不友好，下策。**
- **乐观锁 + CAS**（⭐ Agent 场景最佳锁方案）：数据带版本号，提交时 Compare-And-Swap 校验版本没变才写入并 +1，冲突则重读重试（退避）。不阻塞、并行度高、无死锁，适合「冲突其实不频繁」的 Agent 场景。
- **从源头避免争抢**（更高明）：
  1. **分区写 Sharding**（最实用）：各 Agent 写各自文件（A.json/B.json），Orchestrator 最后合并 → 零冲突。
  2. **Append-only 事件日志**：只追加不改，最终态由重放算出（Event Sourcing）。
  3. **CRDT**：数学保证合并一致的数据结构，重武器，一般用不到。

## 两个必加护栏

1. **锁 / 操作超时**：Agent 崩了锁也自动失效，防卡死全场（时间戳从外部传入，避免不确定性）。
2. **写入 schema 校验**：Agent 会幻觉，脏数据比丢数据更致命。

## 决策表速查

| 场景 | 首选方案 |
| --- | --- |
| Agent 各干各的、结果独立 | **分区写**（首选，零冲突）|
| 只增不改、要审计 | **Append-only 日志** |
| 必须共改、冲突少 | **乐观锁 + CAS**（Agent 最佳）|
| 必须共改、冲突频繁且改动重 | **悲观锁 + 超时**（慎用）|
| 强一致性要求极高 | **CRDT / 事务** |

## 相关

- [[multi-agent-collaboration]] —— 共享黑板是其 IPC 模式之一
- 来源：[[ai-agent-from-tools-to-concurrency]]
