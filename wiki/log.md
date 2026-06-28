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

## 2026-06-28（新增主题：MySQL）
- [更新页面] wiki/concepts/mysql-cheatsheet.md —— 新建 MySQL 常用语法单页速查（DDL/DML/查询/JOIN/子查询/CTE/索引/事务）+ 纯对比表记忆法（四类语句、书写vs执行顺序、WHERE vs HAVING、JOIN 留谁、易错点）。
- [更新页面] wiki/index.md —— 新增 MySQL 主题与概念页入口。
- [说明] 此为通用知识整理，无外部来源/无 raw 原文，页内已标注「建议对照 MySQL 官方文档」；版本相关语法（CTE/窗口函数 8.0+）已标注。

## 2026-06-28（补归档原文）
- [新增资料] raw/clips/ai-agent-from-tools-to-concurrency.md —— 将 AI Agent 原理笔记原文归档到 raw/（此前仅存在于 wiki/sources/），符合「原文进 raw、整理进 wiki」规则，标签 clip。

## 2026-06-25（新增资料：AI Agent 原理笔记）
- [新增资料] wiki/sources/ai-agent-from-tools-to-concurrency.md —— 用户与 Claude 对话沉淀的 AI Agent 原理笔记（已是来源摘要页格式）。补全 source_url 为「待补充（对话沉淀，无外部 URL）」，修正 related_concepts 断链（[[mcp]] → [[claude-code-mcp]]）。
- [更新页面] wiki/concepts/ 新建 6 个概念页：function-calling、ai-agent-loop、llm-as-os、context-engineering、multi-agent-collaboration、agent-concurrency-control。
- [更新页面] wiki/index.md —— 新增「AI Agent 原理」主题、6 个概念页、该来源摘要页入清单。
- [说明] 该笔记原 raw 原文未单独入 raw/（内容直接以 source 形式提供）；如需归档原始对话，可补存到 raw/clips/。

## 2026-06-25（新建综合页）
- [综合] wiki/syntheses/claude-code-全景图.md —— 第一篇综合页，跨 12 篇模块整合，按「核心命题 / 能力分层 / 学习路径 / 组合工作流 / 设计原则 / 待核验」六部分串起全部概念与示例。
- [更新页面] wiki/index.md —— 综合页区填入全景图，当前主题加体系入口。

## 2026-06-25（首次健康检查）
- [健康检查] outputs/health/health-2026-06-25.md —— 首次体检。结论：整体健康，资料/摘要 1:1 全覆盖、无孤立页、无断链、无 clippings 残留。发现 2 个轻微问题（8 个 subagent 文件标签写作 `tags: clip` 非数组、模型版本号 4.6/4.5 已过期需标注来源时点）+ 1 个结构空缺（syntheses 综合页为空）。

## 2026-06-25（深挖第二层：指南内部指向的示例/模板）
- [新增资料] raw/clips/ 新增 10 篇二级资料（标签 clip）：8 个 Subagent 示例定义（code-reviewer、clean-code-reviewer、test-engineer、documentation-writer、secure-reviewer、implementation-agent、debugger、data-scientist）+ planning-mode-examples + checkpoint-examples。
- [说明] Subagent 定义文件原文自带 frontmatter（name/description/tools/model），为避免冲突，来源信息以顶部 HTML 注释保存，未叠加第二个 frontmatter。
- [来源摘要] wiki/sources/ 新增 10 篇来源摘要页，与上面 10 篇一一对应。
- [更新页面] wiki/concepts/claude-code-subagents.md —— 新增「内置示例 subagent 清单」表格，链接 8 个示例。
- [更新页面] wiki/concepts/claude-code-advanced-features.md / claude-code-checkpoints.md —— 各加一条实战示例链接。
- [更新页面] wiki/index.md —— 来源摘要页区新增「二级资料」清单。
- [说明] 仅入库主指南直接指向的二级链接；模块间互引（已入库）与 CLI/官方文档外链未重复抓取。

## 2026-06-25（追加：入库主指南指向的 12 篇文章）
- [新增资料] raw/clips/ 新增 12 篇 claude-howto 文章原文（标签 clip）：10 个教程模块（01-slash-commands ~ 10-cli）+ catalog + learning-roadmap。
- [来源摘要] wiki/sources/ 新增 12 篇来源摘要页，与上面 12 篇原文一一对应。
- [更新页面] wiki/concepts/ 新建 10 个功能概念页：slash-commands、memory、skills、subagents、mcp、hooks、plugins、checkpoints、advanced-features、cli。
- [更新页面] wiki/index.md —— 概念页与来源摘要页清单扩充到全量。
- [说明] 多处保留「待核验」标注（如模型版本号 Opus/Sonnet/Haiku 4.6/4.5、部分 CLI 参数、MCP token 上限命令写法），均因原文存疑或时效性，未擅自当事实写死。

## 2026-06-25
- [新增资料] raw/clips/claude-howto-用一个周末掌握-claude-code.md —— GitHub 开源指南《用一个周末掌握 Claude Code》中文 README，标签 clip。
- [来源摘要] wiki/sources/claude-howto-用一个周末掌握-claude-code.md —— 由上面的 clip 生成。
- [更新页面] wiki/concepts/claude-code.md —— 新建：Claude Code 概念 + 七大核心功能模块。
- [更新页面] wiki/concepts/claude-code-功能组合工作流.md —— 新建：功能组合的典型工作流场景。
- [更新页面] wiki/entities/claude-howto-luongnv89.md —— 新建：开源指南项目实体页。
- [更新页面] wiki/index.md —— 补充当前主题、概念页、实体页、来源摘要页清单。
- [其他] 初始化知识库：创建目录结构、index.md、log.md、AGENTS.md、各模板 README，初始化 Git（main 分支）并配置 GitHub 远程。
