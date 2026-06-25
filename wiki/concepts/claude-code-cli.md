---
title: Claude Code CLI
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code CLI

> Claude Code 的命令行接口，是与 Claude Code 交互的主要方式，区分交互式 REPL 与可脚本化的打印模式。

## 是什么

CLI 是与 Claude Code 交互的主要方式：`claude` 启动交互式 REPL，`claude "query"` 带初始提示启动，`claude -p "query"` 进入打印模式（查询后退出、可脚本化、可管道化、可输出 JSON）。它的核心区分是「交互模式（REPL）」与「打印模式（`-p`）」，并支持模型与配置参数、系统提示词自定义、工具与权限管理、会话管理、MCP 与 Subagents 配置等。来源：[[claude-howto-10-cli]]。

## 关键点

- 会话相关命令：`-c, --continue` 继续最近一次会话，`-r, --resume` 按 ID 或名称恢复，`--from-pr <number>` 恢复与 GitHub PR 关联的会话。
- 模型选择用 `--model`（短名 sonnet/opus/haiku 或完整名），`--fallback-model` 设置后备模型，`opusplan` 别名表示 Opus 规划、Sonnet 执行；`--effort` 设置推理强度（low/medium/high/max，也可用 `/effort` 或 `CLAUDE_EFFORT`）。【Effort 级别对应 Opus 4.6，版本对应关系待核验】
- 系统提示词三个参数：`--system-prompt`（替换整段）、`--system-prompt-file`（从文件加载，仅打印模式）、`--append-system-prompt`（追加）。
- 权限与工具管理：`--tools` 限制内置工具，`--allowedTools`/`--disallowedTools` 控制是否提示，`--permission-mode` 设置权限模式，`--dangerously-skip-permissions` 跳过所有提示。
- 打印模式输出由 `--output-format` 控制（text/json/stream-json），配合 `--json-schema` 获得结构化输出，`--max-budget-usd` 限制单次花费。
- Subagents 用 `--agents`（JSON 或文件）和 `--agent` 配置（必填 `description` 和 `prompt`，可选 `tools`、`model`）；加载优先级：CLI 定义 > 用户级（`~/.claude/agents/`）> 项目级（`.claude/agents/`）。
- 高价值场景：CI/CD 集成（`claude -p --output-format json`）、管道分析日志、批处理（`find ... | xargs claude -p`）、配合 `jq` 解析 JSON；`--bare` 为极简模式，跳过 hooks、skills、plugins、MCP、自动记忆和 `CLAUDE.md`。
- 部分参数（如 `--unsafe`、`--dry-run`、`--list-sessions`）的可用性和版本支持情况待核验，原文以「如果你的版本支持」措辞标注。

## 相关

- [[claude-code]] —— 所属工具
- 来源摘要：[[claude-howto-10-cli]]
