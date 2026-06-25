---
title: 检查点示例 Checkpoint Examples
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/08-checkpoints/checkpoint-examples.md
created: 2026-06-25
tags: [clip]
---

# 检查点示例 Checkpoint Examples

## summary
本文通过 8 个真实场景展示了 Claude Code 检查点（Checkpoint）功能的用法。检查点在每次用户提示时自动创建，用户无需手动保存；通过连续两次 `Esc`（Esc+Esc）或 `/rewind` 可打开检查点浏览器并回退。检查点的核心价值是让用户安全地试验多种激进方案，再挑选最优解保留，最后用 git 落地。

## key_points
- 检查点是自动创建的：每次用户提示都会创建一个检查点，无需手动保存。
- 回退方式：连续按两次 `Esc`（Esc+Esc）或使用 `/rewind`，都可以打开检查点浏览器。
- 恢复时可选择恢复代码、恢复对话、两者都恢复，或「从这里开始总结」。
- 典型用法是从同一基线检查点（Baseline）出发并行尝试多种方案，再回到效果最好的版本，甚至把多个版本的优点组合（示例 2 性能优化最终从 450ms 降到 95ms，提升 79%）。
- 数据库迁移示例：直接迁移方案测试失败后，回退到检查点 A 改试双写模式，验证更稳妥后提交。
- 调试示例：从「Before debugging」检查点出发，依次排除事件监听器、数据库连接两个假设，最终定位到缓存层的循环引用。
- API 设计示例：在 REST、GraphQL 之间反复回退对比，最终选定 REST 方案。
- 长会话可用「从这里开始总结」压缩对话以减少上下文窗口占用，原始消息仍保留在记录里。
- 检查点用于探索，git 用于最终落地，两者结合使用。
- 不要害怕试验：检查点让激进改动变得安全可回退。

## related_concepts
- [[claude-code]]
- [[claude-code-checkpoints]]
