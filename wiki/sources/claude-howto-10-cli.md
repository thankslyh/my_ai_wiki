---
title: Claude Code 教程 10：CLI Reference
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/10-cli/README.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 教程 10：CLI Reference

## summary

本文是 Claude Code 命令行接口（CLI）的完整参考，覆盖了 `claude` 的各类命令、核心标志、模型与配置参数、系统提示词自定义、工具与权限管理、输出格式、会话管理、MCP 配置和 Subagents 配置等。文章的核心区分是「交互模式（REPL）」与「打印模式（`-p`，可脚本化、可管道化、可输出 JSON）」，并给出了大量高价值使用场景，包括 CI/CD 集成、管道式日志分析、多会话工作流、批处理和 JSON API 集成等实战示例。

## key_points

- CLI 是与 Claude Code 交互的主要方式；`claude` 启动交互式 REPL，`claude "query"` 带初始提示启动，`claude -p "query"` 进入打印模式（查询后退出，可脚本化）。
- 会话相关命令：`-c, --continue` 继续最近一次会话，`-r, --resume` 按 ID 或名称恢复会话；还可用 `--from-pr <number>` 恢复与 GitHub PR 关联的会话。
- 模型选择用 `--model`（短名 sonnet/opus/haiku 或完整模型名），`--fallback-model` 设置负载过高时的后备模型，`opusplan` 别名表示 Opus 规划、Sonnet 执行。
- `--effort` 设置推理强度（low/medium/high/max），也可通过 slash command `/effort` 或环境变量 `CLAUDE_EFFORT` 设置；文中标注 Effort 级别对应 Opus 4.6（版本对应关系待核验）。
- 系统提示词三个参数：`--system-prompt`（替换整段，交互+打印均可）、`--system-prompt-file`（从文件加载，仅打印模式）、`--append-system-prompt`（追加，交互+打印均可）。
- 权限与工具管理：`--tools` 限制可用内置工具，`--allowedTools` / `--disallowedTools` 控制是否需要提示，`--permission-mode`（如 plan、auto）设置权限模式，`--dangerously-skip-permissions` 跳过所有提示。
- 打印模式输出格式由 `--output-format` 控制（text/json/stream-json），配合 `--json-schema` 可获得符合 schema 的结构化输出，`--max-budget-usd` 可限制单次花费。
- Subagents 可通过 `--agents`（JSON 定义或文件）和 `--agent`（指定使用）配置；Subagent JSON 必填 `description` 和 `prompt`，可选 `tools` 和 `model`。
- Subagent 加载优先级：CLI 定义（`--agents`）> 用户级（`~/.claude/agents/`）> 项目级（`.claude/agents/`），CLI 定义会覆盖本次会话的用户级和项目级 agents。
- 常用环境变量包括 `ANTHROPIC_API_KEY`、`CLAUDE_MODEL`、`CLAUDE_EFFORT`、`CLAUDE_WORKING_DIRECTORY`、`CLAUDE_OUTPUT_FORMAT`、`CLAUDE_MCP_CONFIG`。
- 高价值场景：CI/CD 集成（`claude -p --output-format json`）、管道分析日志（`cat error.log | claude -p "..."`）、批处理（`find ... | xargs claude -p`）、配合 `jq` 解析 JSON 输出。
- `--bare` 为极简模式，跳过 hooks、skills、plugins、MCP、自动记忆和 `CLAUDE.md`。
- 文中部分参数（如 `--unsafe`、`--dry-run`、`--list-sessions`）的具体可用性和版本支持情况待核验，原文也在故障排查中以「如果你的版本支持」措辞标注。

## related_concepts

- [[claude-code]]
- [[claude-code-cli]]
