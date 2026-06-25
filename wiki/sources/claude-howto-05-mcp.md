---
title: "Claude Code 教程 05：MCP"
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/05-mcp/README.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 教程 05：MCP

## summary
本文介绍 MCP（Model Context Protocol），即 Claude Code 访问外部工具、服务和 API 的标准协议，可把 GitHub、数据库、文件系统、聊天系统等接入 Claude。文章讲解了 MCP 的三段式架构、各类传输方式、配置与作用域管理、把 MCP prompts 暴露成 slash commands，以及用代码执行缓解上下文膨胀的进阶思路，最后给出安全/配置/性能最佳实践与故障排查。

## key_points
- MCP 架构由三部分构成：Claude Code、MCP server、外部工具或数据源；Claude 通过协议向 server 发起工具调用并把结果带回会话。
- 传输方式包括：HTTP（推荐）、stdio（本地）、SSE（已弃用）、WebSocket（实时双向）；并有 OAuth 2.0 认证与 Windows 特殊说明。
- MCP prompts 可暴露为 slash command，格式为 `/mcp__<server-name>__<prompt-name> [arguments]`，例如 `/mcp__github__list_prs`。
- MCP 配置有不同作用域（项目级、用户级），团队共享 server 适合写进项目内并版本化。
- MCP vs Memory 决策矩阵：Memory 适合长期规则、偏好与上下文，MCP 适合实时工具访问与外部数据。
- 进阶能力：MCP 工具搜索、动态工具更新（运行时感知增删）、Elicitation 提示补充、server 去重、`@` 提及引用资源。
- Claude 自身可作为 MCP server 运行（`claude mcp serve`，基于 stdio）；企业可通过受管设置统一分发配置；插件也可打包自带 MCP server。
- 针对上下文膨胀，可把 MCP 当作代码 API 使用，让 Claude 通过工具调用只取回必要数据，减少 round-trip 与 token 浪费；提到了 MCPorter 作为多工具编排运行时。
- MCP 输出过大时可限制 token 或分页；示例提到可将最大输出增大到 50,000 tokens（待核验：原文该命令为占位、未给出具体写法）。
- 安全建议：最小权限、只授权必要工具、检查输出可信度；不要把高风险 token 写死在仓库、不要默认开放所有工具。

## related_concepts
- [[claude-code]]
- [[claude-code-mcp]]
