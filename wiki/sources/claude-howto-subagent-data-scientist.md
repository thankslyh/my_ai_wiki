---
title: Subagent 示例：Data Scientist（数据分析）
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/04-subagents/data-scientist.md
created: 2026-06-25
tags: [clip]
---

# Subagent 示例：Data Scientist（数据分析）

## summary

数据分析 Subagent，擅长 SQL 与 BigQuery，工具 Bash/Read/Write，model 指定为 sonnet（区别于其它 inherit）。

## key_points

- 被调用流程：理解需求 → 写高效 SQL → 用 bq 命令行 → 分析总结 → 清晰呈现。
- SQL 最佳实践：尽早 WHERE 过滤、合适索引、生产避免 SELECT *、探索时限制结果集。
- 分析类型：探索性分析、统计分析、报告（关键指标、环比/同比、管理层总结）。
- 输出含 Objective / Query（带注释）/ Results / Insights / Recommendations。

## related_concepts

- [[claude-code]]
- [[claude-code-subagents]]
- 来源摘要：[[claude-howto-04-subagents]]
