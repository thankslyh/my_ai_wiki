---
title: 计划模式示例 Planning Mode Examples
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/09-advanced-features/planning-mode-examples.md
created: 2026-06-25
tags: [clip]
---

# 计划模式示例 Planning Mode Examples

## summary
本文通过 5 个真实场景展示了在 Claude Code 中使用 `/plan` 计划模式的方式：Claude 在动手编码前先输出按阶段拆解的完整计划，包含步骤、时间预估、风险评估和成功标准，由用户审批（yes/no/modify）后再系统化执行。文章覆盖了构建 REST API、数据库迁移、前端重构、安全实现、性能优化等案例，并总结了计划模式的优势、适用与不适用场景以及最佳实践。

## key_points
- 用法是 `/plan + 任务描述`，Claude 会先产出分阶段计划再执行，每份计划末尾让用户确认（yes/no/modify）。
- 计划通常按阶段（Phase）组织，每阶段列出具体编号步骤，并给出每阶段的预估耗时。
- 计划会包含整体预估（总时间、需创建/修改的文件数、关键技术栈），例如博客 REST API 预估 4.5 小时、约 25 个文件、11 个端点。
- 对高风险任务（如 MongoDB→PostgreSQL 迁移），计划会标注风险等级、回滚策略、关键风险与缓解措施；用户可用 modify 让 Claude 为每个阶段补充回滚方案。
- 计划会写明成功标准，例如迁移要求「零数据丢失、性能回退小于 5%、所有测试通过」。
- 性能优化等案例会给出基线指标与目标指标（如 LCP、FID、CLS、页面加载时间）及各阶段的预期影响。
- 计划模式的六大优势：清晰（路线图）、可估算、风险评估、优先级排序、可审批、可调整。
- 建议始终使用于：多日项目、团队协作、关键系统变更、学习新概念、复杂重构。
- 不建议使用于：修 bug、小改动、简单查询、快速实验。
- 最佳实践包括：审批前仔细审查、发现问题就修改、拆细复杂任务、给现实时间估算、包含回滚策略、写明成功标准、为每个阶段安排测试。

## related_concepts
- [[claude-code]]
- [[claude-code-advanced-features]]
