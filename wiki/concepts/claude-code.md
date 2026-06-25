---
title: Claude Code
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code

> Anthropic 推出的 AI 编程命令行工具（CLI），也提供桌面 / Web / IDE 扩展形态。

## 是什么

Claude Code 是一个交互式 AI 编程助手，从终端输入 `claude` 启动对话开始使用，可逐步进阶到编排 agents、hooks、skills 和 MCP servers，组合成自动化工作流。来源：[[claude-howto-用一个周末掌握-claude-code]]。

## 七大核心功能模块

来源：[[claude-howto-用一个周末掌握-claude-code]]（功能对比表）。

| 功能 | 调用方式 | 持久性 | 最适合 |
| --- | --- | --- | --- |
| **Slash Commands** | 手动 `/cmd` | 仅当前会话 | 快速快捷操作 |
| **Memory** | 自动加载 | 跨会话 | 长期记忆与学习 |
| **Skills** | 自动触发 | 文件系统级 | 自动化工作流 |
| **Subagents** | 自动委派 | 隔离上下文 | 任务拆分 |
| **MCP Protocol** | 自动查询 | 实时 | 获取实时数据 |
| **Hooks** | 事件触发 | 已配置 | 自动化与校验 |
| **Plugins** | 一条命令 | 全功能打包 | 完整解决方案 |

补充模块（来自学习路径）：**Checkpoints**（会话快照与回退）、**Advanced Features**（规划 / 思考 / 后台任务）、**CLI Reference**（命令、参数与选项）。

## 关键认知

- 单独用某个功能只发挥了一小部分能力；**真正的威力来自功能组合**成工作流 → [[claude-code-功能组合工作流]]。
- 支持搭配不同模型使用（`待核验`：原始资料 2026-04 提到 Sonnet 4.6 / Opus 4.6 / Haiku 4.5）。

## 相关

- [[claude-howto-luongnv89]] —— 系统学习它的开源指南
- 来源摘要：[[claude-howto-用一个周末掌握-claude-code]]
