---
title: "Claude Code 教程 06：Hooks"
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/06-hooks/README.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 教程 06：Hooks

## summary
本文介绍 Claude Code 的 Hooks：在特定事件发生时自动执行的 shell 命令，用于格式化、校验、通知、审计等自动化工作，无需手动触发。文章列出了 hook 的分类与事件、安装与 settings.json 配置方式、常见示例脚本，以及最佳实践和故障排查要点。

## key_points
- Hooks 是事件驱动的自动化机制，可理解为 Claude Code 的事件回调，在匹配到事件时自动运行。
- 常见用途：写文件前自动格式化、提交前运行测试、安全扫描、记录 bash 命令、校验用户提示词、发送团队通知。
- Claude Code 提供 4 类、共 25 个事件：Tool Hooks、Session Hooks、Task Hooks、Lifecycle Hooks。
- Tool Hooks 包含 `PreToolUse`、`PostToolUse`、`PostToolUseFailure`、`PermissionRequest`。
- Session Hooks 包含 `SessionStart`、`SessionEnd`、`Stop`、`StopFailure`、`SubagentStart`、`SubagentStop`。
- Task Hooks 包含 `UserPromptSubmit`、`TaskCompleted`、`TaskCreated`、`TeammateIdle`。
- Lifecycle Hooks 包含 `ConfigChange`、`CwdChanged`、`FileChanged`、`PreCompact`、`PostCompact`、`WorktreeCreate`、`WorktreeRemove`、`Notification`、`InstructionsLoaded`、`Elicitation`、`ElicitationResult`。
- 安装方式：把脚本放入 `~/.claude/hooks/` 并赋予可执行权限，再在 `~/.claude/settings.json` 里以 `matcher` + `hooks` 的形式按事件配置。
- 配置示例：`PreToolUse` 匹配 `Write` 触发 `format-code.sh`，`PostToolUse` 匹配 `Write` 触发 `security-scan.sh`。
- 常见示例脚本：`format-code.sh`、`pre-commit.sh`、`security-scan.sh`、`log-bash.sh`、`validate-prompt.sh`、`notify-team.sh`。
- 最佳实践：保持 hook 短小、单一职责、先本地测试、不放复杂业务逻辑、对副作用保持谨慎。

## related_concepts
- [[claude-code]]
- [[claude-code-hooks]]
