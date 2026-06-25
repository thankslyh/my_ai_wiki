---
title: Claude Code Subagents
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code Subagents

> Claude Code 中专门处理某类任务的独立 AI 助手，拥有隔离的上下文、自己的提示词和工具权限。

## 是什么

Subagents 是专门处理某类任务的独立 AI 助手，拥有隔离的上下文、自己的提示词和工具权限，适合把复杂工作拆分给不同角色并行委派。配置文件通常是带 frontmatter 的 Markdown，分项目级 `.claude/agents/` 和用户级 `~/.claude/agents/` 两级。来源：[[claude-howto-04-subagents]]。

## 关键点

- 核心价值在于上下文隔离、角色分工清晰、适合并行与委派。
- 配置文件分两级：项目级 `.claude/agents/`、用户级 `~/.claude/agents/`；常见 frontmatter 字段包括 `name`、`description`、`tools`、`model`、`prompt`、`context`。
- 工具权限可按角色裁剪：审查型建议只读，实现型可适度开放写权限，高风险动作保持人工审批；也可限制 Claude 只能 spawn 某些 subagent 以降低风险。
- 推荐用 `/agents` 命令管理；调用方式有自动委派、显式调用、`@agent-name` 提及、会话级固定使用等多种。
- 进阶能力：可恢复的 agents（长任务接力）、后台 subagents（不阻塞主会话）、worktree 隔离（避免文件状态互相污染）、持久记忆（项目/用户/子目录级范围）。
- Agent Teams 是实验性的多角色协作模式，与侧重单任务委派的 Subagents 区分；需通过设置开启，且功能可能变化。
- 目录提供 8 个示例 subagent：Code Reviewer、Test Engineer、Documentation Writer、Secure Reviewer、Implementation Agent、Debugger、Data Scientist、Clean Code Reviewer。
- 设计原则：单一职责、描述明确、工具权限最小化；system prompt 要具体、不冗长、只保留执行所需信息。

## 相关

- [[claude-code]] —— 所属工具
- [[claude-code-memory]] —— subagents 可拥有自己的持久记忆范围
- [[claude-code-skills]] —— Skills 可委派给 subagent 运行
- 来源摘要：[[claude-howto-04-subagents]]
