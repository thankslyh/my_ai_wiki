---
title: Subagent 示例：Test Engineer（测试工程师）
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/04-subagents/test-engineer.md
created: 2026-06-25
tags: [clip]
---

# Subagent 示例：Test Engineer（测试工程师）

## summary

负责全面测试覆盖的 Subagent，新功能或改动后主动使用，工具含 Write 可写测试文件并运行验证。

## key_points

- 测试策略五类：单元 / 集成 / 端到端 / 边界情况 / 错误场景。
- 覆盖率要求：最低 80%，关键路径（认证、支付、数据处理）要求 100%。
- 要求使用项目现有框架（Jest、pytest 等），mock 外部依赖，含 setup/teardown。
- 输出含 File / Tests 数 / 预计 Coverage 提升 / 覆盖的 Critical Paths。

## related_concepts

- [[claude-code]]
- [[claude-code-subagents]]
- 来源摘要：[[claude-howto-04-subagents]]
