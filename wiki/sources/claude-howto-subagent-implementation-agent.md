---
title: Subagent 示例：Implementation Agent（功能实现）
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/04-subagents/implementation-agent.md
created: 2026-06-25
tags: [clip]
---

# Subagent 示例：Implementation Agent（功能实现）

## summary

全栈实现 Subagent，拥有完整工具权限（Read/Write/Edit/Bash/Grep/Glob），可端到端按规格实现功能。

## key_points

- 实现流程：理解需求 → 分析现有代码模式 → 制定方案 → 逐步实现 → 边做边测 → 清理重构。
- 代码质量要求：遵循项目规范、自解释代码、仅复杂逻辑加注释、函数短小专注。
- 输出含 Files Created / Files Modified / Tests Added / Build Status / Notes。
- 完成前检查清单：符合规范、测试通过、构建成功、无 lint 错误、处理边界、有错误处理。

## related_concepts

- [[claude-code]]
- [[claude-code-subagents]]
- 来源摘要：[[claude-howto-04-subagents]]
