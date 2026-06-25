---
title: 用一个周末掌握 Claude Code
source: GitHub 仓库 luongnv89/claude-howto（zh/README.md）
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/README.md
created: 2026-06-25
tags: [clip]
---

# 用一个周末掌握 Claude Code

## summary

一份开源（MIT 许可）的中文教程式指南，目标是带普通用户在一个周末（完整路径约 11–13 小时）从入门到高级掌握 [[claude-code]]。它不是功能参考手册，而是以 Mermaid 图示、可复制粘贴的生产级模板和递进式学习路径为特色，强调"把多个功能组合成工作流"才是真正的威力来源。原文档版本为 v2.1.112（2026 年 4 月），兼容 Claude Code 2.1+。

## key_points

- 核心定位：教程 + 可视化 + 示例驱动，与官方参考文档互补（先学本指南，再查官方细节）。
- 包含 10 个教程模块，覆盖 Claude Code 全部核心功能，配可直接复制的配置模板。
- 学习路径按水平分层：初学者（Slash Commands，约 2.5h）→ 中级（Skills，约 3.5h）→ 高级（MCP / Hooks，约 5h）。
- 10 模块顺序：Slash Commands → Memory → Checkpoints → CLI Basics → Skills → Hooks → MCP → Subagents → Advanced Features → Plugins。
- 强调"功能组合"：如自动化代码审查 = Slash Commands + Subagents + Memory + MCP；安全审计 = Subagents + Skills + Hooks（只读模式）。
- 内置自测：`/self-assessment` 找水平、`/lesson-quiz [topic]` 查盲点。
- 15 分钟快速上手：克隆仓库 → 复制 slash command → 试运行 → 配 `CLAUDE.md` 项目记忆 → 装一个 skill。
- 所有模板适用于 Claude Sonnet 4.6、Opus 4.6、Haiku 4.5（`待核验`：原文写于 2026-04，与当前最新模型版本可能有出入）。
- 可用 `uv run scripts/build_epub.py` 生成离线 EPUB。

## related_concepts

- [[claude-code]]
- [[claude-howto-luongnv89]]
- [[claude-code-功能组合工作流]]
