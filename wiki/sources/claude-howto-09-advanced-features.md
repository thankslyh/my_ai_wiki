---
title: Claude Code 教程 09：Advanced Features
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/09-advanced-features/README.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 教程 09：Advanced Features

## summary
这是一份 Claude Code 高级能力的完整指南，把基础能力扩展到规划、推理、自动化和控制层面。它系统覆盖了规划模式、扩展思考、自动模式、后台任务、定时任务、权限模式、无头模式、会话管理、交互功能、语音输入、消息通道、Chrome 集成、远程控制、网页会话、桌面应用、任务列表、Git 工作树、沙盒、企业受管设置和配置等多个主题。

## key_points
- Planning Mode 是两阶段流程（先规划生成可审阅计划、批准后再实现）；可用 `/plan`、`claude --permission-mode plan`、设置 `defaultMode: plan`、或 `Shift+Tab`/`Alt+M` 启动；`opusplan` 别名用 Opus 规划、Sonnet 执行；`Ctrl+G` 可在外部编辑器改计划。
- Extended Thinking 让 Claude 给出方案前进行分步推理；对所有模型默认开启（Opus 4.6、Sonnet 4.6、Haiku 4.5）；Opus 4.6 支持自适应推理，effort 等级 low/medium/high/max（max 仅 Opus 4.6）；快捷键 `Option+T`/`Alt+T`。【模型版本号待核验】
- Auto Mode 是 Research Preview：执行每个动作前用后台安全分类器评估风险；用 `claude --enable-auto-mode` 解锁后在 REPL 用 Shift+Tab 切换；无法判定时回退到更保守的权限处理。
- 六种权限模式：`default`、`acceptEdits`、`plan`、`auto`、`dontAsk`、`bypassPermissions`。
- Print/Headless Mode 用 `claude -p` 非交互运行，适合自动化和 CI/CD，支持管道输入、`--output-format json` 结构化输出、限制自主回合数、schema 验证。
- 后台任务让长时间操作（构建/测试/下载/扫描）不阻塞对话，可查看状态、中止、等待完成、恢复上下文。
- 定时任务通过 `/loop`（支持显式间隔与自然语言）和 `/schedule`（一次性提醒）实现，支持云端调度。
- 会话管理命令：`/resume`、`/rename`、`/fork`、`claude -c`（继续上次）、`claude -r`（按名称/ID 恢复）、`--fork`（恢复并分叉）。
- Voice Dictation 支持按住说话和 20 种语言识别；Channels（Research Preview）允许 MCP server 向运行中会话推送消息（支持 Discord、Telegram 等）。
- Remote Control 用 `claude --remote-control` 从 Claude.ai/app 控制本地会话；Web Sessions 用 `claude --remote` 创建、`claude --teleport` 在本地恢复。
- Git Worktrees 用 `claude -w` 在隔离 worktree 中启动，适合并行工作；沙盒提供文件系统和网络隔离（`sandbox.enabled`）。
- 配置文件位置：`~/.claude/settings.json`、`.claude/settings.json`、`.claude/settings.local.json`；环境变量含 `ANTHROPIC_API_KEY`、`CLAUDE_MODEL` 等。

## related_concepts
- [[claude-code]]
- [[claude-code-advanced-features]]
