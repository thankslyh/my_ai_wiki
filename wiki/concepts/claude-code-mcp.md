---
title: Claude Code MCP
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code MCP

> MCP（Model Context Protocol）是 Claude Code 访问外部工具、服务和 API 的标准协议。

## 是什么
MCP 是一套标准协议，让 Claude Code 能把 GitHub、数据库、文件系统、聊天系统等外部工具与数据源接入会话。其架构由三部分构成：Claude Code、MCP server、外部工具或数据源；Claude 通过协议向 server 发起工具调用，再把结果带回会话。来源：[[claude-howto-05-mcp]]。

## 关键点
- 架构为三段式：Claude Code、MCP server、外部工具或数据源，工具调用结果会带回会话。来源：[[claude-howto-05-mcp]]
- 传输方式包括 HTTP（推荐）、stdio（本地）、SSE（已弃用）、WebSocket（实时双向），并有 OAuth 2.0 认证与 Windows 特殊说明。来源：[[claude-howto-05-mcp]]
- MCP prompts 可暴露为 slash command，格式为 `/mcp__<server-name>__<prompt-name> [arguments]`，例如 `/mcp__github__list_prs`。来源：[[claude-howto-05-mcp]]
- 配置有不同作用域（项目级、用户级）；团队共享 server 适合写进项目内并版本化。来源：[[claude-howto-05-mcp]]
- MCP vs Memory：Memory 适合长期规则、偏好与上下文，MCP 适合实时工具访问与外部数据。来源：[[claude-howto-05-mcp]]
- 安全建议：最小权限、只授权必要工具、检查输出可信度，不要把高风险 token 写死在仓库。来源：[[claude-howto-05-mcp]]
- MCP 输出过大时可限制 token 或分页；示例提到可将最大输出增大到 50,000 tokens（待核验：原文该命令为占位、未给出具体写法）。来源：[[claude-howto-05-mcp]]

## 相关
- [[claude-code]] —— 所属工具
- [[claude-code-plugins]] —— 插件可打包自带 MCP server
- 来源摘要：[[claude-howto-05-mcp]]
