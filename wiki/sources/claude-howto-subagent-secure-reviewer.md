---
title: Subagent 示例：Secure Reviewer（安全审查，最小权限）
source: GitHub 仓库 luongnv89/claude-howto
source_url: https://github.com/luongnv89/claude-howto/blob/main/zh/04-subagents/secure-reviewer.md
created: 2026-06-25
tags: [clip]
---

# Subagent 示例：Secure Reviewer（安全审查，最小权限）

## summary

安全审查 Subagent，采用最小权限设计：工具仅 Read/Grep，不能执行代码、不能改文件、不能跑测试，确保审计过程不破坏任何东西。

## key_points

- 安全审查五大重点：身份验证、授权、数据暴露、注入漏洞（SQL/命令/XSS/LDAP）、配置问题。
- 提供现成 grep 搜索模式定位硬编码密钥、SQL 注入风险、命令注入风险。
- 输出每个漏洞含 Severity / Type（OWASP 类别）/ Location / Description / Risk / Remediation。
- 是「只读模式安全审计」工作流的核心组件（对应 README 的安全审计场景）。

## related_concepts

- [[claude-code]]
- [[claude-code-subagents]]
- 来源摘要：[[claude-howto-04-subagents]]
