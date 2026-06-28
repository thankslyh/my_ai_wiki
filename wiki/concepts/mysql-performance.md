---
title: MySQL 性能优化
type: concept
created: 2026-06-28
tags: [concept, mysql, database, performance]
---

# MySQL 性能优化

> 从「定位慢查询 → 看懂 EXPLAIN → 优化索引/SQL/分页 → 表结构与配置」的优化路径。配纯对比表记忆法。
> 来源：通用知识整理，非外部资料。以 MySQL 8.0 / InnoDB 为准，引用前建议对照 [MySQL 官方文档](https://dev.mysql.com/doc/)。
> 语法速查见 [[mysql-cheatsheet]]。

---

## 一、定位慢查询（先找到病灶）

| 手段 | 说明 |
| --- | --- |
| 慢查询日志 | `SET GLOBAL slow_query_log=ON;` `SET GLOBAL long_query_time=1;`（>1s 记录） |
| 查看执行计划 | `EXPLAIN SELECT ...;`（最常用） |
| 更详细分析 | `EXPLAIN ANALYZE SELECT ...;`（8.0+，含真实耗时） |
| 当前运行的查询 | `SHOW PROCESSLIST;` |
| 统计信息 | `SHOW STATUS LIKE 'Slow_queries';` |

> 优化第一原则：**先测量，再优化**。不要凭感觉加索引。

---

## 二、看懂 EXPLAIN（最核心技能）

重点看这几列：

| 列 | 含义 | 关注点 |
| --- | --- | --- |
| `type` | 访问类型 | 性能排序见下表，至少要到 `range` |
| `key` | 实际用到的索引 | 为 NULL 说明没走索引 |
| `rows` | 预估扫描行数 | 越小越好 |
| `Extra` | 额外信息 | 出现 `Using filesort` / `Using temporary` 要警惕 |

### type 性能等级（从好到差，重点记）

| type | 含义 | 评价 |
| --- | --- | --- |
| `system` / `const` | 主键/唯一索引等值查询，最多一行 | 最优 |
| `eq_ref` | 连表时用主键/唯一索引 | 很好 |
| `ref` | 普通索引等值查询 | 好 |
| `range` | 索引范围扫描（BETWEEN/>/IN） | 可接受 |
| `index` | 扫描整个索引树 | 较差 |
| `ALL` | **全表扫描** | 最差，重点优化对象 |

### Extra 警示信号

| Extra | 含义 | 应对 |
| --- | --- | --- |
| `Using index` | 覆盖索引，不回表 | ✅ 好事 |
| `Using where` | 用 WHERE 过滤 | 正常 |
| `Using filesort` | 额外排序（非索引排序） | ⚠️ 给 ORDER BY 列加索引 |
| `Using temporary` | 用了临时表（常见于 GROUP BY） | ⚠️ 优化分组/索引 |

---

## 三、索引优化

| 原则 | 说明 |
| --- | --- |
| 最左前缀 | 联合索引 `(a,b,c)`，查询条件要从 a 开始才命中（详见 [[mysql-cheatsheet]]） |
| 覆盖索引 | SELECT 的列都在索引里 → 不回表，看到 `Using index` |
| 区分度高的列建索引 | 性别（只有男女）建索引几乎无用 |
| 联合索引列顺序 | 等值列在前、范围列在后；区分度高的在前 |
| 避免冗余索引 | `(a)` 已被 `(a,b)` 覆盖，无需再单独建 `(a)` |
| 控制索引数量 | 索引加速查询但拖慢写入、占空间，不是越多越好 |

### 索引失效场景（重点记）

| 场景 | 反例 | 正解 |
| --- | --- | --- |
| 列上用函数/运算 | `WHERE YEAR(created)=2024` | `WHERE created >= '2024-01-01' AND created < '2025-01-01'` |
| 前导模糊 | `WHERE name LIKE '%张'` | `LIKE '张%'`（右模糊可走索引） |
| 隐式类型转换 | `WHERE phone = 138...`（phone 是 varchar 却传数字） | 传字符串 `'138...'` |
| OR 一侧无索引 | `WHERE a=1 OR b=2`（b 无索引） | 给 b 也加索引，或用 UNION |
| 不等于/NOT | `WHERE a != 1` / `NOT IN` | 改写为范围或 IN |
| 违反最左前缀 | 联合索引 `(a,b)` 却只查 b | 调整索引或查询 |

---

## 四、SQL 改写优化

| 问题 | 优化 |
| --- | --- |
| `SELECT *` | 只查需要的列（利于覆盖索引、减少传输） |
| 深分页 `LIMIT 1000000,10` | 用游标：`WHERE id > 上次最大id LIMIT 10`（见下） |
| 子查询慢 | 多数场景改 JOIN 更快 |
| `COUNT(*)` 大表很慢 | 可接受估算时用 `EXPLAIN` 的 rows，或维护计数表 |
| 大批量操作锁表 | 分批处理（每次 1000 行） |
| 函数包裹索引列 | 把计算挪到等号右边 |

### 深分页优化（高频考点）

```sql
-- ❌ 慢：要扫描并丢弃前 100 万行
SELECT * FROM t ORDER BY id LIMIT 1000000, 10;

-- ✅ 快：游标分页（记住上一页最后的 id）
SELECT * FROM t WHERE id > 1000000 ORDER BY id LIMIT 10;

-- ✅ 或：先用覆盖索引定位 id 再回表
SELECT * FROM t INNER JOIN (
  SELECT id FROM t ORDER BY id LIMIT 1000000, 10
) tmp USING (id);
```

---

## 五、表结构 & 配置

| 方向 | 要点 |
| --- | --- |
| 字段类型 | 够用就好：能 `INT` 不 `BIGINT`，能 `VARCHAR(50)` 不 `VARCHAR(255)`；金额用 `DECIMAL` |
| NOT NULL | 尽量加 NOT NULL（NULL 占空间、影响索引、聚合易出错） |
| 主键 | 用自增 `BIGINT` 或有序主键，避免随机 UUID 导致页分裂 |
| 拆分 | 大字段（TEXT/BLOB）拆到单独表，避免拖慢主表 |
| 分库分表 | 单表数据量过大（千万级+）再考虑，不要过早 |
| 连接池 | 复用连接，避免频繁建连开销 |
| 缓冲池 | `innodb_buffer_pool_size` 是 InnoDB 最重要参数（一般设物理内存 50-70%） |

---

## 六、记忆法（纯对比表）

### 1. 优化排查顺序（口诀：测 → 看 → 改 → 调）

| 步骤 | 动作 | 工具 |
| --- | --- | --- |
| 测 | 找出慢查询 | 慢查询日志 / SHOW PROCESSLIST |
| 看 | 分析执行计划 | EXPLAIN（看 type/key/rows/Extra） |
| 改 | 优化索引与 SQL | 加索引 / 改写 SQL / 优化分页 |
| 调 | 表结构与配置 | 字段类型 / buffer pool / 分表 |

### 2. EXPLAIN 的 type「保底线」

> 一句话：**至少到 `range`，看到 `ALL`（全表）就要优化**。
> 顺序记忆：`const` > `ref` > `range` > `index` > `ALL`（越靠右越慢）。

### 3. 索引「建不建」对比

| 适合建索引 | 不适合建索引 |
| --- | --- |
| WHERE / JOIN / ORDER BY 常用列 | 区分度低的列（性别、状态） |
| 区分度高的列 | 频繁更新的列 |
| 需要覆盖索引的查询 | 很小的表（全表扫描更快） |

### 4. 索引失效「八字诀」

> **模糊、函数、转换、或非**——
> 前导**模糊**、列上**函数**、隐式**转换**、**或**(OR无索引)、**非**(!=/NOT) 都可能失效。

---

## 相关

- [[mysql-cheatsheet]] —— MySQL 常用语法速查（索引/事务基础语法）
- 来源：通用知识整理（建议对照 [MySQL 官方文档](https://dev.mysql.com/doc/)）
