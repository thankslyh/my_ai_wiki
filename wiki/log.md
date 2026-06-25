# 变更日志 / Log

> 记录每次：新增资料、编译资料、更新页面、健康检查结果。
> 倒序排列，最新在最上面。每条尽量写明日期、动作、涉及文件。

---

## 格式约定

```
## YYYY-MM-DD
- [新增资料] raw/<类型>/<文件名> —— 一句话说明
- [来源摘要] wiki/sources/<页名> —— 由哪份原始资料生成
- [更新页面] wiki/concepts/<页名> —— 改了什么
- [健康检查] outputs/health/<报告名> —— 主要结论
```

动作类型：`新增资料` `来源摘要` `更新页面` `综合` `健康检查` `其他`

---

## 2026-06-25
- [新增资料] raw/clips/claude-howto-用一个周末掌握-claude-code.md —— GitHub 开源指南《用一个周末掌握 Claude Code》中文 README，标签 clip。
- [来源摘要] wiki/sources/claude-howto-用一个周末掌握-claude-code.md —— 由上面的 clip 生成。
- [更新页面] wiki/concepts/claude-code.md —— 新建：Claude Code 概念 + 七大核心功能模块。
- [更新页面] wiki/concepts/claude-code-功能组合工作流.md —— 新建：功能组合的典型工作流场景。
- [更新页面] wiki/entities/claude-howto-luongnv89.md —— 新建：开源指南项目实体页。
- [更新页面] wiki/index.md —— 补充当前主题、概念页、实体页、来源摘要页清单。
- [其他] 初始化知识库：创建目录结构、index.md、log.md、AGENTS.md、各模板 README，初始化 Git（main 分支）并配置 GitHub 远程。
