---
title: Claude Code Skills
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code Skills

> Claude Code 中可复用、可自动触发的能力包，核心机制是按需分层加载的「渐进式披露」。

## 是什么

Agent Skills 是可复用、可自动触发的能力包，一个 skill 通常包含 `SKILL.md`、参考文件、脚本和模板，放在正确的目录结构里即被自动发现。核心机制是「渐进式披露」：Skills 按需分三层加载，而非一次性塞满上下文。来源：[[claude-howto-03-skills]]。

## 关键点

- Skill 通常由 `SKILL.md`、参考文件、脚本和模板组成，Claude 会在合适场景自动加载。
- 渐进式披露分三层：先只看描述判断相关性，再加载 `SKILL.md` 读核心说明，最后按需加载支持文件（脚本、模板、参考资料）。
- Skills 可放在项目目录 `.claude/skills/` 或用户目录 `~/.claude/skills/`。
- `SKILL.md` 必填字段为 `name` 和 `description`；可选字段包括 `argument-hint`、`allowed-tools`、`model`、`disable-model-invocation`、`user-invocable`、`context`、`agent`、`hooks`。
- 通过 `disable-model-invocation`、`user-invocable` 和工具白名单可控制 Claude 是否能自动调用某个 skill；支持 `$ARGUMENTS`、`$0`、`$1` 等参数替换和 `` !`command` `` 注入。
- 最佳实践：描述要具体并包含触发词、一个 skill 只解决一个问题、`SKILL.md` 尽量控制在 500 行以内、把重复内容移到支持文件。
- 与其他功能对比：Skills 自动/半自动触发适合复用与流程标准化，Slash Commands 手动触发，Subagents 自动委派隔离任务，Hooks 事件触发用于自动化与验证。
- 安全注意：不在 skill 中硬编码密钥，对副作用操作保持用户触发，给自动触发的 skill 设清晰边界。

## 相关

- [[claude-code]] —— 所属工具
- [[claude-code-slash-commands]] —— 自定义命令已合并进 Skills
- [[claude-code-subagents]] —— Subagents 用于自动委派隔离任务
- 来源摘要：[[claude-howto-03-skills]]
