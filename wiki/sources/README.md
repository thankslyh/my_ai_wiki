# 来源摘要页模板 / Source Summary Template

> 每份进入 `raw/` 的原始资料，都要在 `wiki/sources/` 下生成一篇来源摘要页。
> 复制下面的模板，文件名建议用 `来源标题-简短slug.md`。

---

## 模板

```markdown
---
title:            # 资料标题
source:           # 来源类型 / 出处（如：微信公众号「xxx」、arXiv、某博客）
source_url:       # 原文链接（没有就写 待补充）
created:          # 收录日期 YYYY-MM-DD
tags:             # 与所在 raw 目录一致：article / wechat / clip / paper
---

# {{title}}

## summary
<!-- 用 2-5 句话概括这份资料讲了什么 -->

## key_points
<!-- 列出关键观点 / 结论 / 数据，每条尽量可独立引用 -->
-
-
-

## related_concepts
<!-- 关联的概念页 / 实体页 / 综合页，用 [[wiki 链接]] -->
-
```

---

## 字段说明

| 字段 | 含义 |
| --- | --- |
| `title` | 资料标题 |
| `source` | 来源 / 出处（平台、机构、作者等） |
| `source_url` | 原文链接；缺失标 `待补充` |
| `created` | 收录日期 |
| `summary` | 内容概要 |
| `key_points` | 关键观点列表 |
| `related_concepts` | 关联的 wiki 页面（用 `[[ ]]` 链接） |

> 拿不准的信息标 `待核验`，缺失的标 `待补充`，不要编造。
