---
title: Claude Code Memory
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code Memory

> Claude Code 的跨会话上下文保留机制，以 `CLAUDE.md` 为载体在合适时机自动加载。

## 是什么

Memory 让 Claude 在不同会话之间保留上下文。把团队规范、项目规则、个人偏好和目录级约束写进 `CLAUDE.md`，Claude 会按层级和优先级在合适时机自动加载。核心命令有 `/init`、`/memory`、`#` 三个。来源：[[claude-howto-02-memory]]。

## 关键点

- 三个核心命令：`/init` 初始化项目级 `CLAUDE.md`，`/memory` 打开记忆编辑器，`#` 前缀快速把一条规则写入记忆。
- 记忆分层级：受管策略（组织级）、项目记忆（`./CLAUDE.md`）、目录记忆（子目录）、用户记忆（`~/.claude/CLAUDE.md`）。
- 优先级规则：更具体、更接近当前上下文的记忆优先——组织级优先于普通偏好，项目规则优先于个人偏好，目录级规则优先于项目级通用规则。
- Auto memory 会根据当前工作目录、父目录和已配置路径逐层查找并加载相关记忆文件；可用 `--add-dir` 把额外目录加入可见范围。
- 支持模块化规则：通过 YAML frontmatter 设置路径规则，并可用子目录和 symlink 复用局部规则。
- 可通过 `claudeMdExcludes` 之类的设置排除不应自动加载的 `CLAUDE.md`（确切配置键名待核验）。
- 最佳实践：项目记忆存团队标准、目录记忆存局部差异，先写简洁规则再补充；不要把 README 整份复制进 `CLAUDE.md`。
- Subagents 可拥有自己的记忆范围（具体行为细节待补充）。

## 相关

- [[claude-code]] —— 所属工具
- [[claude-code-subagents]] —— subagents 可拥有自己的记忆范围
- 来源摘要：[[claude-howto-02-memory]]
