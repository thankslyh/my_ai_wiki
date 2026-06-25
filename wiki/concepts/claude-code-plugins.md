---
title: Claude Code Plugins
type: concept
created: 2026-06-25
tags: [concept]
---

# Claude Code Plugins

> 插件是 Claude Code 最高级别的扩展方式，把 slash commands、subagents、MCP servers 和 hooks 打包成可一条命令安装的完整方案。

## 是什么
插件把 slash commands、subagents、MCP servers、hooks 四类能力组合在一起，通过一条命令安装。它让完整工作流可以一次安装、团队共享、版本控制和分发。插件清单使用 `.claude-plugin/plugin.json` 的 JSON 格式，包含 name、description、version、author 等字段。来源：[[claude-howto-07-plugins]]。

## 关键点
- 把 slash commands、subagents、MCP servers、hooks 四类能力组合在一起，一条命令安装。来源：[[claude-howto-07-plugins]]
- 分为四种类型：官方（Anthropic 维护）、社区、组织（团队内部）、个人。来源：[[claude-howto-07-plugins]]
- 清单使用 `.claude-plugin/plugin.json`；插件市场定义在 `.claude-plugin/marketplace.json`，官方市场是 `anthropics/claude-plugins-official`。来源：[[claude-howto-07-plugins]]
- 来源支持相对路径、GitHub、Git URL、Git 子目录、npm、pip 六种类型，GitHub/git 来源支持 `ref` 和 `sha` 做版本锁定。来源：[[claude-howto-07-plugins]]
- 插件 subagents 运行在受限沙箱中，定义里**不允许**使用 `hooks`、`mcpServers`、`permissionMode` 三个 frontmatter 键，确保不越权。来源：[[claude-howto-07-plugins]]
- 本地开发用 `claude --plugin-dir ./my-plugin` 测试（可重复指定多个），并支持热重载 `/reload-plugins`。来源：[[claude-howto-07-plugins]]
- 版本特性：v2.1.83+ 支持 `userConfig`（`sensitive: true` 的值存入系统钥匙串）、v2.1.78+ 提供 `${CLAUDE_PLUGIN_DATA}` 持久化目录、v2.1.80+ 支持用 `source: 'settings'` 内联定义插件。来源：[[claude-howto-07-plugins]]

## 相关
- [[claude-code]] —— 所属工具
- [[claude-code-mcp]] —— 插件可打包自带 MCP server
- [[claude-code-hooks]] —— 插件可打包自带 hooks
- 来源摘要：[[claude-howto-07-plugins]]
