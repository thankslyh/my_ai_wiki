---
title: Claude Code 教程 07：Plugins
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/07-plugins/README.md
created: 2026-06-25
tags: [clip]
---

# Claude Code 教程 07：Plugins

## summary
插件是 Claude Code 最高级别的扩展方式，把 slash commands、subagents、MCP servers 和 hooks 打包成可一条命令安装的完整方案。它让完整工作流可以一次安装、团队共享、版本控制和分发。文章详细讲解了插件的定义结构（`.claude-plugin/plugin.json`）、目录组织、市场分发机制、安装与生命周期管理，以及安全限制和最佳实践。

## key_points
- 插件把 slash commands、subagents、MCP servers、hooks 四类能力组合在一起，通过一条命令安装。
- 插件分为四种类型：官方（Anthropic 维护）、社区、组织（团队内部）、个人。
- 插件清单使用 `.claude-plugin/plugin.json` 的 JSON 格式，包含 name、description、version、author 等字段。
- 插件可包含 LSP server 配置（`.lsp.json` 或 plugin.json 内联 `lsp` 键），提供实时诊断、代码导航、悬浮信息、符号列表；官方市场已预配置 pyright-lsp、typescript-lsp、rust-lsp。
- v2.1.83+ 支持在清单中用 `userConfig` 声明用户可配置选项，标记 `sensitive: true` 的值会存入系统钥匙串而非明文。
- v2.1.78+ 提供 `${CLAUDE_PLUGIN_DATA}` 持久化状态目录，每个插件唯一并跨会话保留，卸载前一直保留。
- v2.1.80+ 支持用 `source: 'settings'` 在设置文件中内联定义插件，无需单独仓库或市场。
- 插件市场定义在 `.claude-plugin/marketplace.json`；官方市场是 `anthropics/claude-plugins-official`。
- 插件来源支持相对路径、GitHub、Git URL、Git 子目录、npm、pip 六种类型，GitHub/git 来源支持 `ref` 和 `sha` 做版本锁定。
- 插件 subagents 运行在受限沙箱中，定义里**不允许**使用 `hooks`、`mcpServers`、`permissionMode` 三个 frontmatter 键，确保不越权。
- 本地开发用 `claude --plugin-dir ./my-plugin` 测试（可重复指定多个），并支持热重载 `/reload-plugins`。
- 对比手动配置（2+ 小时）vs 插件安装（2 分钟）：插件可让团队复现完全相同的设置。

## related_concepts
- [[claude-code]]
- [[claude-code-plugins]]
