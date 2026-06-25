---
title: Claude Code 功能目录 CATALOG
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/CATALOG.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 功能目录 CATALOG

## summary

本文是 Claude Code 全部功能的快速参考目录，把功能划分为七大类：Slash Commands、Subagents、Skills、Plugins、MCP Servers、Hooks 和 Memory Files，并以表格形式给出每类的内置项、示例项与安装方式。文章还汇总了 6 种权限模式、25 个 Hook 事件、7 种 Memory 类型，以及「2026 年 3 月新功能」清单，最后给出功能选择指南、安装优先级和一条命令完成全部安装的脚本。

## key_points

- 功能总览：Slash Commands（55+ 内置）、Subagents（6 内置）、Skills（5 内置）、Plugins、MCP Servers（1 内置）、Hooks（25 个事件）、Memory（7 种类型），合计统计为 117 项（内置 99 + 示例 43，原文表格如此列示，加总口径待核验）。
- 七大功能的定位区分：Slash Command 手动立即触发、Memory 自动加载持久上下文、Skill 自动触发的能力包、Subagent 隔离上下文的专门任务、MCP Server 访问外部实时数据、Hook 事件驱动自动化、Plugin 把以上打包成一体化解决方案。
- 6 种权限模式：`default`（每次询问）、`acceptEdits`（自动接受编辑）、`plan`（只读）、`auto`（完全自主，Research Preview）、`bypassPermissions`（跳过所有检查）、`dontAsk`（跳过需权限的工具）。
- 6 个内置 Subagents：general-purpose、Plan、Explore（Haiku 4.5）、Bash、statusline-setup（Sonnet 4.6）、Claude Code Guide（Haiku 4.5），各有不同的工具集和模型。
- 5 个内置 Skills：`/simplify`、`/batch`、`/debug`、`/loop`、`/claude-api`。
- Hooks 共 25 个事件，涵盖 SessionStart、PreToolUse、PostToolUse、PermissionRequest、SubagentStart/Stop、PreCompact/PostCompact、WorktreeCreate/Remove、Elicitation 等，可在事件发生时执行自动化。
- 7 种 Memory 类型：Managed Policy（组织）、Project（`./CLAUDE.md`）、Project Rules（`.claude/rules/`）、User（`~/.claude/CLAUDE.md`）、User Rules（`~/.claude/rules/`）、Local（`./CLAUDE.local.md`，截至 2026 年 3 月不在官方文档中，可能是历史遗留）、Auto Memory（自动）。
- 常见 MCP Servers 示例包括 GitHub、Database、Filesystem、Slack、Google Docs、Asana、Stripe、Memory，以及内置的 Context7（库文档）。
- 「2026 年 3 月新功能」清单包含 Remote Control、Web Sessions、Desktop App、Agent Teams、Task List、Git Worktrees、Sandboxing、MCP OAuth、Scheduled Tasks、Chrome Integration、自动模式（Research Preview）、Channels（Research Preview）、语音输入、Agent/Prompt Hook 类型、WebSocket MCP Transport 等。
- 安装优先级建议：1. Memory（必装）→ 2. Slash Commands → 3. Subagents → 4. Hooks → 5. MCP Servers → 6. Plugins。
- 文档标注最后更新于 2026 年 4 月 9 日，对应 Claude Code 版本 2.1.97。

## related_concepts

- [[claude-code]]
