---
title: Claude Code Hooks
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code Hooks

> Hooks 是在特定事件发生时自动执行的 shell 命令，用于格式化、校验、通知、审计等自动化工作。

## 是什么
Hooks 是 Claude Code 的事件驱动自动化机制，可理解为事件回调：在匹配到事件时自动运行指定 shell 命令，无需手动触发。常见用途包括写文件前自动格式化、提交前运行测试、安全扫描、记录 bash 命令、校验用户提示词、发送团队通知。来源：[[claude-howto-06-hooks]]。

## 关键点
- 事件驱动的自动化，匹配到事件时自动运行，相当于 Claude Code 的事件回调。来源：[[claude-howto-06-hooks]]
- 提供 4 类、共 25 个事件：Tool Hooks、Session Hooks、Task Hooks、Lifecycle Hooks。来源：[[claude-howto-06-hooks]]
- Tool Hooks 包含 `PreToolUse`、`PostToolUse`、`PostToolUseFailure`、`PermissionRequest`。来源：[[claude-howto-06-hooks]]
- 安装方式：脚本放入 `~/.claude/hooks/` 并赋予可执行权限，再在 `~/.claude/settings.json` 里以 `matcher` + `hooks` 形式按事件配置。来源：[[claude-howto-06-hooks]]
- 配置示例：`PreToolUse` 匹配 `Write` 触发 `format-code.sh`，`PostToolUse` 匹配 `Write` 触发 `security-scan.sh`。来源：[[claude-howto-06-hooks]]
- 最佳实践：保持 hook 短小、单一职责、先本地测试、不放复杂业务逻辑、对副作用保持谨慎。来源：[[claude-howto-06-hooks]]

## 相关
- [[claude-code]] —— 所属工具
- [[claude-code-plugins]] —— 插件可打包自带 hooks
- 来源摘要：[[claude-howto-06-hooks]]
