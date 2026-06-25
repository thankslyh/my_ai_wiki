---
title: Claude Code 教程 02：Memory
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/02-memory/README.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 教程 02：Memory

## summary

本文介绍 Claude Code 的 Memory 机制，它让 Claude 在不同会话之间保留上下文。通过把团队规范、项目规则、个人偏好和目录级约束写进 `CLAUDE.md`，Claude 会在合适时机自动加载。文章讲解了 `/init`、`/memory`、`#` 三个核心命令，记忆的多层级体系（受管策略、项目、目录、用户），以及 auto memory、模块化规则、`--add-dir` 和最佳实践等内容。

## key_points

- Memory 的作用是跨会话保留上下文，载体是 `CLAUDE.md`。
- 三个核心命令：`/init` 初始化项目级 `CLAUDE.md`，`/memory` 打开记忆编辑器，`#` 前缀快速把一条规则写入记忆。
- 记忆分层级：受管策略（组织级）、项目记忆（`./CLAUDE.md`）、目录记忆（子目录）、用户记忆（`~/.claude/CLAUDE.md`）。
- 优先级规则：更具体、更接近当前上下文的记忆优先——组织级优先于普通偏好，项目规则优先于个人偏好，目录级规则优先于项目级通用规则。
- 可通过 `claudeMdExcludes` 之类的设置排除不应自动加载的 `CLAUDE.md`（确切配置键名待核验）。
- Auto memory 让 Claude 根据当前工作目录、父目录和已配置路径逐层查找并加载相关记忆文件。
- 支持模块化规则：通过 YAML frontmatter 设置路径规则，并可用子目录和 symlink 复用局部规则。
- 可用 `--add-dir` 把额外目录加入 Claude 的可见范围，适合多目录协作。
- 最佳实践：用项目记忆存团队标准、目录记忆存局部差异，先写简洁规则再补充；不要把 README 整份复制进 `CLAUDE.md`，不要让记忆变成垃圾桶。
- Subagents 可拥有自己的记忆范围（具体行为细节待补充）。

## related_concepts

- [[claude-code]]
- [[claude-code-memory]]
