---
title: Claude Code 教程 01：Slash Commands
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/01-slash-commands/README.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 教程 01：Slash Commands

## summary

本文系统梳理了 Claude Code 中 slash command 的体系，分为内置命令、Skills、插件命令和 MCP prompts 四类。文章给出了 55+ 个内置命令的速查表，并重点说明自定义 slash command 已经合并进 Skills——`.claude/commands/` 仍可用，但官方更推荐 `.claude/skills/`。此外还涵盖了 frontmatter 字段、参数传递、shell 动态上下文注入、文件引用以及命令的创建、安装与故障排查。

## key_points

- Slash command 分为四类：内置命令（如 `/help`、`/clear`、`/model`）、Skills（自定义，基于 `SKILL.md`）、插件命令（如 `/frontend-design:frontend-design`）、MCP prompts（如 `/mcp__github__list_prs`）。
- 自定义 slash command 已合并进 Skills；`.claude/commands/<name>.md` 仍可用，但推荐迁移到 `.claude/skills/<name>/SKILL.md`。
- 当 skill 与 command 同名时，skill 优先。
- Claude Code 目前提供 55+ 个内置命令和 5 个内置 Skills；在会话中输入 `/` 可查看并筛选全部命令。
- 内置 Skills 包括 `/batch`、`/claude-api`、`/debug`、`/loop`、`/simplify`，调用方式与 slash command 一致。
- 部分命令已弃用或更名：`/review` 被 `code-review` 插件替代；`/output-style` 自 v2.1.73 弃用；`/fork` 在 v2.1.77 更名为 `/branch`（别名仍可用）；`/vim` 自 v2.1.92 移除，改用 `/config → Editor mode`。
- `/effort` 的 `max` 级别需要 Opus 4.6（版本对应关系待核验）。
- Skill 的 frontmatter 字段包括 `name`、`description`、`argument-hint`、`allowed-tools`、`model`、`disable-model-invocation`、`user-invocable`、`context`、`agent`、`hooks`。
- 命令支持参数注入：`$ARGUMENTS` 接收全部参数，`$0`、`$1` 等接收单个参数；可用 `` !`command` `` 注入 shell 输出，用 `@` 引用文件内容。
- 对有副作用的命令应设置 `disable-model-invocation: true`，避免 Claude 自动触发。
- 文档标注最后更新于 2026 年 4 月 9 日，对应 Claude Code 版本 2.1.97。

## related_concepts

- [[claude-code]]
- [[claude-code-slash-commands]]
