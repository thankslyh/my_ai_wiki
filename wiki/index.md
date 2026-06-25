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

- [[claude-code]] —— Claude Code 是什么 + 七大核心功能模块
- [[claude-code-功能组合工作流]] —— 多功能组合成自动化流水线的典型场景

## 实体页

- [[claude-howto-luongnv89]] —— 开源 Claude Code 学习指南项目（luongnv89）

## 综合页

> 暂无。

## 来源摘要页

- [[claude-howto-用一个周末掌握-claude-code]] —— GitHub 开源指南《用一个周末掌握 Claude Code》中文版

详见 [[wiki/sources/README]] 模板。

---

## 维护入口

- 维护规则：[[AGENTS]]
- 变更日志：[[wiki/log]]
- 来源摘要模板：[[wiki/sources/README]]
- 健康检查说明：[[outputs/health/README]]
