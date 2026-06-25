---
title: Subagent 示例：Debugger（排错专家）
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/04-subagents/debugger.md
created: 2026-06-25
tags: [clip]
---

# Subagent 示例：Debugger（排错专家）

## summary

擅长根因分析的排错 Subagent，遇到错误/测试失败/异常行为时主动使用，工具 Read/Edit/Bash/Grep/Glob。

## key_points

- 排错流程：分析错误与日志 → 检查最近代码变更（git diff）→ 提出并测试假设 → 隔离故障 → 最小修复并验证。
- 强调实施「最小修复」并检查回归问题。
- 输出含 Error / Root Cause / Evidence / Fix / Testing / Prevention。
- 提供常用调试命令（git diff、grep 错误模式、跑指定测试）。

## related_concepts

- [[claude-code]]
- [[claude-code-subagents]]
- 来源摘要：[[claude-howto-04-subagents]]
