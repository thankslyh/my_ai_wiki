---
title: Subagent 示例：Clean Code Reviewer（整洁代码审查）
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/04-subagents/clean-code-reviewer.md
created: 2026-06-25
tags: [clip]
---

# Subagent 示例：Clean Code Reviewer（整洁代码审查）

## summary

专注 Robert C. Martin《Clean Code》原则的审查 Subagent，识别违规并给可执行修复，工具 Read/Grep/Glob/Bash。

## key_points

- 检查重点：命名、函数（<20 行、单一职责、≤3 参数）、注释、结构、SOLID、DRY/KISS/YAGNI、错误处理、坏味道。
- 严重级别按函数行数/参数数/嵌套层数划分 Critical/High/Medium/Low。
- 核心理念：代码被阅读次数是写作的 10 倍，优化可读性而非炫技。
- 输出格式含 Summary 统计 + Violations（带 file:line + 代码片段 + 修复）+ Good Practices。
- 明确跳过：生成代码、配置文件、测试夹具。

## related_concepts

- [[claude-code]]
- [[claude-code-subagents]]
- 来源摘要：[[claude-howto-04-subagents]]
