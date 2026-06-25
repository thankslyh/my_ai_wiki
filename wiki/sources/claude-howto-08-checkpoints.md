---
title: Claude Code 教程 08：Checkpoints
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/08-checkpoints/README.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 教程 08：Checkpoints

## summary
Checkpoints 与 Rewind 能力让你保存对话状态并在 Claude Code 会话中回退到之前的时间点，方便探索不同方案、修复错误或比较多个实现路径。每个 checkpoint 是对话状态快照（消息、文件修改、工具历史、会话上下文），由 Claude Code 在每次用户提示时自动创建。文章强调它的价值在于让试错变安全，但它是会话级回退工具，不是 git 的替代品。

## key_points
- Checkpoint 是对话快照，包含所有已交换的消息、已做的文件修改、工具使用历史和当前会话上下文。
- 三个核心概念：Checkpoint（快照）、Rewind（回退并丢弃之后的更改）、Branch Point（从同一 checkpoint 出发探索多个方案）。
- 两种访问方式：按两次 `Esc`（Esc+Esc）打开界面，或使用 `/rewind` 命令（别名 `/checkpoint`）。
- Rewind 菜单有五个选项：恢复代码和对话、只恢复对话、只恢复代码、从这里开始总结（压缩为 AI 摘要且原始消息保留）、算了（取消）。
- 自动创建机制：每次用户提示创建一个 checkpoint，跨会话持久保存，30 天后自动清理旧 checkpoint。
- 可在设置中用 `autoCheckpoint`（默认 `true`）开关每次提示后的自动 checkpoint。
- 典型场景：探索不同方案、安全重构、A/B 测试、错误恢复。
- 局限性：checkpoints 适合会话级回退，不是版本控制系统，也不跟踪外部文件系统变化；长期保存/审计/共享仍需 git。
- 与 git 互补：checkpoints 用于会话内快速试错，git 用于永久保存最终方案。
- 何时该 rewind 的信号：方案变复杂且方向未定、测试刚失败、想比较两种实现、想保留干净起点继续探索。

## related_concepts
- [[claude-code]]
- [[claude-code-checkpoints]]
