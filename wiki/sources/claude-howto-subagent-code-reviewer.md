---
title: Subagent 示例：Code Reviewer（代码审查专家）
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/04-subagents/code-reviewer.md
created: 2026-06-25
tags: [clip]
---

# Subagent 示例：Code Reviewer（代码审查专家）

## summary

claude-howto 提供的 Subagent 定义模板，定位为资深代码审查员。被调用时先跑 git diff 看变更再审查，工具限定 Read/Grep/Glob/Bash，model 为 inherit。

## key_points

- frontmatter 配置：name=code-reviewer，tools=Read,Grep,Glob,Bash，model=inherit。
- 审查优先级（按序）：安全 > 性能 > 代码质量 > 测试覆盖率 > 设计模式。
- 被调用流程：运行 git diff → 聚焦改动文件 → 立即开始审查。
- 输出每个问题含：Severity / Category / Location / Issue / Suggested Fix / Impact。
- 反馈按 Critical（必须修）→ Warnings（应该修）→ Suggestions（可改进）组织。

## related_concepts

- [[claude-code]]
- [[claude-code-subagents]]
- 来源摘要：[[claude-howto-04-subagents]]
