---
title: Claude Code Slash Commands
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code Slash Commands

> Claude Code 中以 `/` 触发的命令体系，涵盖内置命令、Skills、插件命令和 MCP prompts 四类。

## 是什么

Slash Commands 是在 Claude Code 会话中输入 `/` 调用的命令，分为四类：内置命令（如 `/help`、`/clear`、`/model`）、Skills（自定义，基于 `SKILL.md`）、插件命令（如 `/frontend-design:frontend-design`）和 MCP prompts（如 `/mcp__github__list_prs`）。自定义 slash command 已合并进 [[claude-code-skills]]，`.claude/commands/<name>.md` 仍可用，但官方推荐迁移到 `.claude/skills/<name>/SKILL.md`。来源：[[claude-howto-01-slash-commands]]。

## 关键点

- 命令分四类：内置命令、Skills、插件命令、MCP prompts；会话中输入 `/` 可查看并筛选全部命令。
- 自定义 slash command 已合并进 Skills；`.claude/commands/` 仍可用，但推荐用 `.claude/skills/`。当 skill 与 command 同名时，skill 优先。
- 目前提供 55+ 个内置命令和 5 个内置 Skills（`/batch`、`/claude-api`、`/debug`、`/loop`、`/simplify`）。
- 部分命令已弃用或更名：`/review` 被 `code-review` 插件替代；`/output-style` 自 v2.1.73 弃用；`/fork` 在 v2.1.77 更名为 `/branch`；`/vim` 自 v2.1.92 移除，改用 `/config → Editor mode`。
- 支持参数与上下文注入：`$ARGUMENTS` 接收全部参数，`$0`、`$1` 等接收单个参数；`` !`command` `` 注入 shell 输出，`@` 引用文件内容。
- 对有副作用的命令应设 `disable-model-invocation: true`，避免 Claude 自动触发。
- `/effort` 的 `max` 级别需要 Opus 4.6（版本对应关系待核验）。

## 相关

- [[claude-code]] —— 所属工具
- [[claude-code-skills]] —— 自定义命令已合并进 Skills
- 来源摘要：[[claude-howto-01-slash-commands]]
