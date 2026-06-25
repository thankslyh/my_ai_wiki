# 知识库索引 / Index

> 这是整个知识库的入口页，说明当前收录了哪些主题、资料和导航入口。
> 每次新增或整理资料后，记得回来更新这里。

---

## 这是什么

基于 [Karpathy LLM Wiki](https://github.com/karpathy/llm.c) 思路搭建的个人 Markdown 知识库：
用文件夹 + Markdown + Obsidian + Git 跑通最小闭环，不做企业级 RAG、不上复杂数据库。

工作流：**原始资料进 `raw/` → 生成来源摘要页 → 提炼概念/实体/综合页 → 更新本页与日志**。

---

## 目录导航

| 目录 | 用途 |
| --- | --- |
| `raw/articles/` | 原始文章（标签 `article`，微信公众号追加 `wechat`） |
| `raw/papers/` | 原始论文（标签 `paper`） |
| `raw/clips/` | 网页剪藏 / 摘录（标签 `clip`） |
| `wiki/sources/` | 来源摘要页（每份原始资料对应一篇） |
| `wiki/concepts/` | 概念页（抽象知识点） |
| `wiki/entities/` | 实体页（人物、组织、产品、模型等） |
| `wiki/syntheses/` | 综合页（跨来源的主题整合与观点） |
| `outputs/qa/` | 问答产物 |
| `outputs/health/` | 健康检查报告 |

---

## 当前主题

- **Claude Code** — Anthropic 的 AI 编程 CLI，及其功能组合工作流 → [[claude-code]]

---

## 概念页

总览：
- [[claude-code]] —— Claude Code 是什么 + 七大核心功能模块
- [[claude-code-功能组合工作流]] —— 多功能组合成自动化流水线的典型场景

七大核心功能 + 进阶模块：
- [[claude-code-slash-commands]] —— 手动触发的快捷命令
- [[claude-code-memory]] —— 跨会话持久记忆（CLAUDE.md）
- [[claude-code-skills]] —— 自动触发的可复用能力
- [[claude-code-subagents]] —— 隔离上下文的专门化助手
- [[claude-code-mcp]] —— 接入外部工具/实时数据的协议
- [[claude-code-hooks]] —— 事件驱动的自动化与校验
- [[claude-code-plugins]] —— 打包后的完整功能集合
- [[claude-code-checkpoints]] —— 会话快照与回退
- [[claude-code-advanced-features]] —— 规划/思考/后台任务
- [[claude-code-cli]] —— 命令、参数与选项

## 实体页

- [[claude-howto-luongnv89]] —— 开源 Claude Code 学习指南项目（luongnv89）

## 综合页

> 暂无。

## 来源摘要页

主指南：
- [[claude-howto-用一个周末掌握-claude-code]] —— 总览《用一个周末掌握 Claude Code》

10 个教程模块：
- [[claude-howto-01-slash-commands]] · [[claude-howto-02-memory]] · [[claude-howto-03-skills]] · [[claude-howto-04-subagents]] · [[claude-howto-05-mcp]] · [[claude-howto-06-hooks]] · [[claude-howto-07-plugins]] · [[claude-howto-08-checkpoints]] · [[claude-howto-09-advanced-features]] · [[claude-howto-10-cli]]

其它：
- [[claude-howto-catalog]] —— 功能目录 CATALOG
- [[claude-howto-learning-roadmap]] —— 学习路线图

二级资料（指南内部指向的示例 / 模板）：
- 8 个 Subagent 示例定义：[[claude-howto-subagent-code-reviewer]] · [[claude-howto-subagent-clean-code-reviewer]] · [[claude-howto-subagent-test-engineer]] · [[claude-howto-subagent-documentation-writer]] · [[claude-howto-subagent-secure-reviewer]] · [[claude-howto-subagent-implementation-agent]] · [[claude-howto-subagent-debugger]] · [[claude-howto-subagent-data-scientist]]
- 实战示例：[[claude-howto-planning-mode-examples]] · [[claude-howto-checkpoint-examples]]

详见 [[wiki/sources/README]] 模板。

---

## 维护入口

- 维护规则：[[AGENTS]]
- 变更日志：[[wiki/log]]
- 来源摘要模板：[[wiki/sources/README]]
- 健康检查说明：[[outputs/health/README]]
