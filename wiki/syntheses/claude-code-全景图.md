---
title: Claude Code 全景图
type: synthesis
created: 2026-06-25
tags: [synthesis]
---

# Claude Code 全景图

> 跨 [[claude-howto-luongnv89]] 全部 12 篇模块整合而成的体系地图：把 [[claude-code]] 的零散功能，按「学习顺序 → 能力分层 → 组合工作流」三条线串起来。
> 来源：本页结论均来自 [[claude-howto-用一个周末掌握-claude-code]] 及其各模块来源摘要页，引用见各处链接。

---

## 一、核心命题

单独用某个功能，只发挥了 Claude Code 一小部分能力；**真正的威力来自把多个功能组合成自动化工作流**。
这条主线贯穿整份指南 → 见 [[claude-code-功能组合工作流]]。

整个体系可以浓缩成一句话：
**用 [[claude-code-slash-commands|命令]] 触发、靠 [[claude-code-memory|记忆]] 持久、由 [[claude-code-skills|技能]] 自动化、向 [[claude-code-subagents|子代理]] 委派、经 [[claude-code-mcp|MCP]] 连外部、用 [[claude-code-hooks|钩子]] 自动管控、以 [[claude-code-plugins|插件]] 打包分发，再以 [[claude-code-checkpoints|检查点]] 兜底试错。**

---

## 二、能力分层（按「触发方式 + 持久性」理解）

来源：[[claude-code]] 七大功能对比表。

| 层 | 功能 | 触发 | 持久性 | 一句话 |
| --- | --- | --- | --- | --- |
| 交互层 | [[claude-code-slash-commands]] | 手动 `/cmd` | 当前会话 | 把常用操作收成快捷命令 |
| 记忆层 | [[claude-code-memory]] | 自动加载 | 跨会话 | `CLAUDE.md` 让上下文持久 |
| 能力层 | [[claude-code-skills]] | 自动触发 | 文件系统级 | 可复用的自动化能力 |
| 委派层 | [[claude-code-subagents]] | 自动委派 | 隔离上下文 | 把任务分给专门角色 |
| 连接层 | [[claude-code-mcp]] | 自动查询 | 实时 | 接外部工具与实时数据 |
| 管控层 | [[claude-code-hooks]] | 事件触发 | 已配置 | 在生命周期节点自动校验 |
| 打包层 | [[claude-code-plugins]] | 一条命令 | 全功能打包 | 把以上能力打包分发 |

**横切能力**（不属于单一层，服务全局）：
- [[claude-code-checkpoints]] —— 会话快照与回退，让试错安全（不是 git 替代品）
- [[claude-code-advanced-features]] —— 规划模式、扩展思考、后台/定时任务、权限模式、无头模式等
- [[claude-code-cli]] —— 命令、参数与选项的底座

---

## 三、推荐学习路径

来源：[[claude-howto-learning-roadmap]]、[[claude-code]]。完整路径约 11–13 小时，按水平递进：

1. **入门**（约 2.5h）：[[claude-code-slash-commands]] → [[claude-code-memory]] → [[claude-code-cli]]
2. **中级**（约 3.5h）：[[claude-code-skills]] → [[claude-code-hooks]] → [[claude-code-checkpoints]]
3. **进阶**（约 5h）：[[claude-code-mcp]] → [[claude-code-subagents]] → [[claude-code-advanced-features]] → [[claude-code-plugins]]

> 顺序原则：先掌握单个功能，再练组合。每学完一个模块用 `/lesson-quiz [topic]` 查盲点。

---

## 四、组合工作流（功能如何协同）

来源：[[claude-code-功能组合工作流]]。典型场景与所需功能：

| 场景 | 功能组合 |
| --- | --- |
| 自动化代码审查 | Slash Commands + Subagents + Memory + MCP |
| 安全审计（只读） | Subagents + Skills + Hooks |
| CI/CD 自动化 | CLI + Hooks + 后台任务 |
| 文档生成 | Skills + Subagents + Plugins |
| 复杂重构 | Checkpoints + 规划模式 + Hooks |
| DevOps 流水线 | Plugins + MCP + Hooks + 后台任务 |

**落地示例**（指南直接提供、已入库）：
- 代码审查可直接复用现成 subagent → [[claude-howto-subagent-code-reviewer]]、[[claude-howto-subagent-clean-code-reviewer]]
- 安全审计用最小权限只读 subagent → [[claude-howto-subagent-secure-reviewer]]
- 测试 / 文档 / 实现 / 排错 / 数据分析 → [[claude-howto-subagent-test-engineer]]、[[claude-howto-subagent-documentation-writer]]、[[claude-howto-subagent-implementation-agent]]、[[claude-howto-subagent-debugger]]、[[claude-howto-subagent-data-scientist]]
- 规划模式实战 → [[claude-howto-planning-mode-examples]]
- 检查点实战 → [[claude-howto-checkpoint-examples]]
- 全部 8 个示例 subagent 的清单见 [[claude-code-subagents]]

---

## 五、几条贯穿全局的设计原则

从各模块归纳出的共性（来源：各概念页）：

- **权限最小化**：subagent / hook 按需裁剪工具权限，审查型只读、实现型才开写权限。见 [[claude-code-subagents]]、[[claude-howto-subagent-secure-reviewer]]。
- **人审关口**：高风险动作保留人工审批；规划模式「先批准计划再执行」。见 [[claude-code-advanced-features]]。
- **可回退**：每次提示自动建 checkpoint，试错不怕翻车。见 [[claude-code-checkpoints]]。
- **可复用 + 可分发**：能力沉淀为 skill，再用 plugin 打包共享。见 [[claude-code-skills]]、[[claude-code-plugins]]。

---

## 六、待核验事项（引用前请注意）

- 资料中的模型版本号（`Opus 4.6 / Sonnet 4.6 / Haiku 4.5`）来自原文 2026-04，**已可能过期**（当前已有更新版本），引用时请标注时点。详见 [[health-2026-06-25]]。
- 部分 CLI 参数、MCP token 上限命令写法、`/effort max` 与模型对应关系等标了 `待核验`，待对照官方文档核实。

---

## 相关

- 工具总览：[[claude-code]]
- 核心理念：[[claude-code-功能组合工作流]]
- 来源指南：[[claude-howto-luongnv89]]、[[claude-howto-用一个周末掌握-claude-code]]
- 首次体检：[[health-2026-06-25]]
