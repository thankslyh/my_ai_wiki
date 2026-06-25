---
title: Claude Code 教程 03：Skills
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/03-skills/README.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 教程 03：Skills

## summary

本文讲解 Claude Code 的 Agent Skills——可复用、可自动触发的能力包，一个 skill 通常包含 `SKILL.md`、参考文件、脚本和模板。核心机制是「渐进式披露」：Skills 按需分三层加载，而非一次性塞满上下文。文章覆盖了 skill 的目录结构、`SKILL.md` 格式与 frontmatter 字段、调用控制、参数替换、subagent 运行，以及多种实战示例、最佳实践、故障排查与共享分发方式。

## key_points

- Skill 是可复用、可自动触发的能力包，通常由 `SKILL.md`、参考文件、脚本和模板组成，Claude 会在合适场景自动加载。
- 渐进式披露分三层：先只看描述判断相关性，再加载 `SKILL.md` 读核心说明，最后按需加载支持文件（脚本、模板、参考资料）。
- Skills 可放在项目目录 `.claude/skills/` 或用户目录 `~/.claude/skills/`，目录结构正确即被自动发现。
- `SKILL.md` 必填字段为 `name` 和 `description`；可选字段包括 `argument-hint`、`allowed-tools`、`model`、`disable-model-invocation`、`user-invocable`、`context`、`agent`、`hooks`。
- 通过 `disable-model-invocation`、`user-invocable` 和工具白名单可控制 Claude 是否能自动调用某个 skill。
- 支持 `$ARGUMENTS`、`$0`、`$1` 等参数替换，以及用 `` !`command` `` 注入 shell 命令结果。
- 最佳实践：描述要具体并包含触发词、一个 skill 只解决一个问题、`SKILL.md` 尽量控制在 500 行以内、把重复内容移到支持文件。
- 与其他功能对比：Skills 自动/半自动触发适合复用与流程标准化，Slash Commands 手动触发，Subagents 自动委派隔离任务，Hooks 事件触发用于自动化与验证。
- 安全注意：不在 skill 中硬编码密钥，对副作用操作保持用户触发，给自动触发的 skill 设清晰边界。
- 共享方式：项目 skills 团队共享、个人 skills 放 `~/.claude/skills`、也可作为插件的一部分分发。

## related_concepts

- [[claude-code]]
- [[claude-code-skills]]
