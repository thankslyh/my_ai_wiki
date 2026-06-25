---
title: Subagent 示例：Documentation Writer（文档撰写）
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/04-subagents/documentation-writer.md
created: 2026-06-25
tags: [clip]
---

# Subagent 示例：Documentation Writer（文档撰写）

## summary

技术文档撰写 Subagent，负责 API 文档、用户指南、架构文档、changelog，工具 Read/Write/Grep。

## key_points

- 文档标准：清晰、含示例、完整（覆盖所有参数与返回值）、结构一致、按实际代码验证准确性。
- API 文档章节：描述、参数、返回值、错误、示例（curl/JS/Python）、相关端点。
- 功能文档章节：概述、前置条件、分步说明、预期结果、故障排查、相关主题。
- 输出含 Type / File / Sections / Examples 数。

## related_concepts

- [[claude-code]]
- [[claude-code-subagents]]
- 来源摘要：[[claude-howto-04-subagents]]
