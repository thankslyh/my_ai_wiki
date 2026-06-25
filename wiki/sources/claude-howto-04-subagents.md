---
title: "Claude Code 教程 04：Subagents"
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/04-subagents/README.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 教程 04：Subagents

## summary
本文是 Claude Code Subagents 的完整参考。Subagents 是专门处理某类任务的独立 AI 助手，拥有隔离的上下文、自己的提示词和工具权限，适合把复杂工作拆分给不同角色。文章覆盖了配置格式、文件位置、内置 subagents、管理与调用方式，以及后台执行、worktree 隔离、持久记忆、Agent Teams（实验性）等进阶特性，最后给出设计原则与若干示例 subagent。

## key_points
- Subagent 的核心价值在于上下文隔离、角色分工清晰、适合并行与委派，便于把复杂任务拆开。
- 配置文件位置分两级：项目级 `.claude/agents/`，用户级 `~/.claude/agents/`。
- Subagent 通常是带 frontmatter 的 Markdown 文件，常见字段包括 `name`、`description`、`tools`、`model`、`prompt`、`context`。
- 工具权限可按角色裁剪：审查型 subagent 建议只读，实现型可适度开放写权限，高风险动作保持人工审批。
- 推荐用 `/agents` 命令管理 subagents；也可直接创建目录与文件，或用 `claude agents` CLI 查看。
- 调用方式有多种：自动委派、显式调用、`@agent-name` 提及、会话级固定使用。
- 进阶能力包括：可恢复的 agents（长任务接力）、后台 subagents（不阻塞主会话）、worktree 隔离（避免文件状态互相污染）、subagent 持久记忆（项目/用户/子目录级范围）。
- 可以限制 Claude 只能 spawn 某些 subagent 以降低风险（如只允许审查类、禁止高风险自动化）。
- Agent Teams 是实验性的多角色协作模式，与侧重单任务委派的 Subagents 区分；需通过设置开启，且功能可能变化。
- 本目录提供 8 个示例 subagent：Code Reviewer、Test Engineer、Documentation Writer、Secure Reviewer、Implementation Agent、Debugger、Data Scientist、Clean Code Reviewer。
- 设计原则：单一职责、描述明确、工具权限最小化；system prompt 要具体、不冗长、只保留执行所需信息。

## related_concepts
- [[claude-code]]
- [[claude-code-subagents]]
