---
title: Claude Code Advanced Features
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code Advanced Features

> Claude Code 在规划、推理、自动化和控制层面的一组高级能力，把基础能力扩展到更复杂的工作流。

## 是什么

Advanced Features 是一组把 Claude Code 基础能力扩展到规划、推理、自动化和控制层面的高级功能，系统覆盖规划模式、扩展思考、自动模式、后台任务、定时任务、权限模式、无头模式、会话管理、语音输入、消息通道、远程控制、Git 工作树、沙盒与配置等多个主题。它们让 Claude Code 从单次对话工具升级为可规划、可自动化、可受控的开发助手。来源：[[claude-howto-09-advanced-features]]。

## 关键点

- Planning Mode 是两阶段流程（先规划生成可审阅计划、批准后再实现）；可用 `/plan`、`claude --permission-mode plan`、设置 `defaultMode: plan` 或 `Shift+Tab`/`Alt+M` 启动；`opusplan` 别名用 Opus 规划、Sonnet 执行。
- Extended Thinking 让 Claude 给出方案前进行分步推理，对所有模型默认开启，effort 等级 low/medium/high/max（max 仅 Opus 4.6），快捷键 `Option+T`/`Alt+T`。【模型版本号待核验】
- 六种权限模式：`default`、`acceptEdits`、`plan`、`auto`、`dontAsk`、`bypassPermissions`；Auto Mode 是 Research Preview，执行每个动作前用后台安全分类器评估风险。
- Print/Headless Mode 用 `claude -p` 非交互运行，适合自动化和 CI/CD，支持管道输入、`--output-format json`、限制自主回合数、schema 验证。
- 后台任务让长时间操作不阻塞对话；定时任务通过 `/loop`（含自然语言间隔）和 `/schedule`（一次性提醒）实现。
- 会话管理命令：`/resume`、`/rename`、`/fork`、`claude -c`（继续上次）、`claude -r`（按名称/ID 恢复）、`--fork`（恢复并分叉）。
- 远程与隔离能力：Remote Control（`claude --remote-control`）、Web Sessions（`claude --remote` 创建、`claude --teleport` 本地恢复）、Git Worktrees（`claude -w` 隔离启动）、沙盒（`sandbox.enabled` 文件系统与网络隔离）。
- 配置文件位置：`~/.claude/settings.json`、`.claude/settings.json`、`.claude/settings.local.json`；环境变量含 `ANTHROPIC_API_KEY`、`CLAUDE_MODEL` 等。

## 相关

- [[claude-code]] —— 所属工具
- 来源摘要：[[claude-howto-09-advanced-features]]
