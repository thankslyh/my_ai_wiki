---
title: Claude Code 学习路线图
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/LEARNING-ROADMAP.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 学习路线图

## summary

本文是 luongnv89/claude-howto 仓库的 Claude Code 学习路线图，提供一份按节奏掌握各项功能的指南。文章先用一个 8 题的自我评估测验把学习者分为三个水平（Beginner / Intermediate / Advanced），再按「依赖关系、复杂度、使用频率」三原则给出 11 步的完整学习顺序和分级里程碑。每个里程碑都配有实战练习、成功标准和下一步，并附带快速开始路径、学习风格建议、进度追踪清单和常见学习难题的解法。

## key_points

- 路线图核心是「先做自我评估再选起点」：8 个勾选项对应三档水平——0-2 项为 Level 1 Beginner、3-5 项为 Level 2 Intermediate、6-8 项为 Level 3 Advanced；也可在 Claude Code 中运行 `/self-assessment` 做交互式测验。
- 学习顺序遵循三原则：依赖关系（先学基础）、复杂度（先易后难）、使用频率（先学最常用），仓库文件夹也按此编号。
- 完整路线共 11 步：Slash Commands → Memory → Checkpoints → CLI Basics → Skills → Hooks → MCP → Subagents → Advanced Features → Plugins → CLI Mastery，总学习时间约 11-13 小时。
- Level 1（约 3 小时）含里程碑 1A「第一个命令与 Memory」（Slash Commands + Memory）和 1B「安全探索」（Checkpoints + CLI Basics）。
- Level 2（约 5 小时）含里程碑 2A「自动化」（Skills + Hooks）和 2B「集成」（MCP + Subagents），强调自动化、外部服务集成与任务委派。
- Level 3（约 5 小时）含里程碑 3A「高级功能」（Planning、Permissions、Extended Thinking、Auto Mode、Channels、语音输入、Remote/Desktop/Web）和 3B「团队与分发」（Plugins + CLI 精通 + CI/CD）。
- 每个里程碑都遵循「你将完成什么 → 实战练习 → 成功标准 → 下一步」结构，并提示用 `/lesson-quiz [lesson]` 检验对应主题的理解。
- 文中重申 6 种权限模式（default、acceptEdits、plan、auto、dontAsk、bypassPermissions）、25 个 Hook 事件与 4 种 Hook 类型（command、http、prompt、agent）、6 个内置 subagent 等关键数字。
- 提供三条快速开始路径：15 分钟（装一个 slash command 见效）、1 小时（搭基础生产力工具）、一个周末（覆盖大部分功能并构建团队 plugin）。
- 针对四类学习风格（视觉型、动手型、阅读型、社交型）和六个常见学习难题给出了具体建议，并附 Beginner/Intermediate/Advanced 三级进度追踪清单。
- 文档标注最后更新于 2026 年 3 月，维护者为 Claude How-To Contributors，许可证为「仅供学习与参考」。

## related_concepts

- [[claude-code]]
- [[claude-howto-luongnv89]]
