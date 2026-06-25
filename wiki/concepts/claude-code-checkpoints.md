---
title: Claude Code Checkpoints
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code Checkpoints

> Claude Code 的会话级状态快照与回退能力，让你保存对话状态并回退到之前的时间点，安全地试错。

## 是什么

Checkpoint 是对话状态的快照，包含已交换的消息、已做的文件修改、工具使用历史和当前会话上下文，由 Claude Code 在每次用户提示时自动创建。配合 Rewind 能力，你可以回退到之前的时间点，方便探索不同方案、修复错误或比较多个实现路径。它的价值在于让试错变安全，但它是会话级回退工具，不是 git 的替代品。来源：[[claude-howto-08-checkpoints]]。

## 关键点

- 三个核心概念：Checkpoint（快照）、Rewind（回退并丢弃之后的更改）、Branch Point（从同一 checkpoint 出发探索多个方案）。
- 两种访问方式：按两次 `Esc`（Esc+Esc）打开界面，或使用 `/rewind` 命令（别名 `/checkpoint`）。
- Rewind 菜单有五个选项：恢复代码和对话、只恢复对话、只恢复代码、从这里开始总结（压缩为 AI 摘要且原始消息保留）、算了（取消）。
- 自动创建机制：每次用户提示创建一个 checkpoint，跨会话持久保存，30 天后自动清理旧 checkpoint；可在设置中用 `autoCheckpoint`（默认 `true`）开关。
- 局限性：适合会话级回退，不是版本控制系统，也不跟踪外部文件系统变化；长期保存、审计、共享仍需 git，二者互补。
- 何时该 rewind 的信号：方案变复杂且方向未定、测试刚失败、想比较两种实现、想保留干净起点继续探索。

## 相关

- [[claude-code]] —— 所属工具
- 来源摘要：[[claude-howto-08-checkpoints]]
