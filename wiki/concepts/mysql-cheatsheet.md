---
title: MySQL 常用语法速查
type: concept
created: 2026-06-28
tags: [concept, mysql, database]
---

# MySQL 常用语法速查

> 单页速查表：覆盖 DDL / DML / 查询 / 索引 / 事务等常用语法，配纯对比表格式记忆法。
> 来源：通用知识整理，非外部资料。语法以 MySQL 8.0 为准，标注「8.0+」的为新版本特性，引用前建议对照 [MySQL 官方文档](https://dev.mysql.com/doc/)。

---

## 一、DDL（数据定义：建库建表改结构）

| 操作 | 语法 |
| --- | --- |
| 建库 | `CREATE DATABASE db DEFAULT CHARSET utf8mb4;` |
| 删库 | `DROP DATABASE db;` |
| 建表 | `CREATE TABLE t (id INT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(50) NOT NULL);` |
| 删表 | `DROP TABLE t;` |
| 清空表（保留结构，重置自增） | `TRUNCATE TABLE t;` |
| 加列 | `ALTER TABLE t ADD COLUMN age INT;` |
| 改列类型 | `ALTER TABLE t MODIFY age BIGINT;` |
| 改列名+类型 | `ALTER TABLE t CHANGE age user_age INT;` |
| 删列 | `ALTER TABLE t DROP COLUMN age;` |
| 改表名 | `RENAME TABLE t TO t2;` |

常用字段类型：`INT` / `BIGINT` / `DECIMAL(10,2)`（精确金额）/ `VARCHAR(n)` / `TEXT` / `DATETIME` / `TIMESTAMP` / `JSON`（5.7+）。

> ⚠️ 金额用 `DECIMAL` 不用 `FLOAT/DOUBLE`（浮点有精度误差）。

---

## 二、DML（数据操作：增删改）

| 操作 | 语法 |
| --- | --- |
| 插入 | `INSERT INTO t (name, age) VALUES ('a', 18);` |
| 批量插入 | `INSERT INTO t (name) VALUES ('a'), ('b'), ('c');` |
| 存在则更新（需唯一键） | `INSERT INTO t (id,name) VALUES (1,'a') ON DUPLICATE KEY UPDATE name='a';` |
| 更新 | `UPDATE t SET age = 20 WHERE id = 1;` |
| 删除 | `DELETE FROM t WHERE id = 1;` |

> ⚠️ `UPDATE` / `DELETE` 不带 `WHERE` 会操作全表，生产慎之又慎。

---

## 三、查询（DQL）

### 基础

```sql
SELECT col1, col2 FROM t
WHERE 条件
GROUP BY col
HAVING 聚合条件
ORDER BY col DESC
LIMIT 10 OFFSET 20;   -- 跳过 20 条取 10 条
```

### WHERE 常用操作符

| 类别 | 写法 |
| --- | --- |
| 比较 | `= != > >= < <=` |
| 范围 | `BETWEEN 1 AND 10` |
| 集合 | `IN (1,2,3)` / `NOT IN (...)` |
| 模糊 | `LIKE 'a%'`（a 开头）/ `LIKE '%a%'`（含 a） |
| 空值 | `IS NULL` / `IS NOT NULL`（不能用 `= NULL`） |
| 逻辑 | `AND` / `OR` / `NOT` |

### 聚合函数

`COUNT(*)` / `SUM(col)` / `AVG(col)` / `MAX(col)` / `MIN(col)`，常配 `GROUP BY`。

### JOIN 连接

| 类型 | 含义 | 语法 |
| --- | --- | --- |
| INNER JOIN | 两表都匹配（交集） | `A INNER JOIN B ON A.id=B.aid` |
| LEFT JOIN | 左表全留，右表无则 NULL | `A LEFT JOIN B ON A.id=B.aid` |
| RIGHT JOIN | 右表全留，左表无则 NULL | `A RIGHT JOIN B ON A.id=B.aid` |
| CROSS JOIN | 笛卡尔积（每行配每行） | `A CROSS JOIN B` |

> MySQL 没有 `FULL OUTER JOIN`，需用 `LEFT JOIN ... UNION ... RIGHT JOIN` 模拟。

### 子查询 & CTE

```sql
-- 子查询
SELECT * FROM t WHERE id IN (SELECT aid FROM b WHERE x = 1);

-- CTE 公用表表达式（8.0+，比嵌套子查询更可读）
WITH hot AS (SELECT aid FROM b WHERE x = 1)
SELECT * FROM t WHERE id IN (SELECT aid FROM hot);

-- 窗口函数（8.0+）：排名不分组
SELECT name, ROW_NUMBER() OVER (PARTITION BY dept ORDER BY salary DESC) rk FROM emp;
```

### UNION

`UNION`（去重）/ `UNION ALL`（不去重，更快）——纵向合并两个结果集，列数与类型需一致。

---

## 四、索引

| 操作 | 语法 |
| --- | --- |
| 建普通索引 | `CREATE INDEX idx_name ON t (name);` |
| 建唯一索引 | `CREATE UNIQUE INDEX idx_name ON t (name);` |
| 建联合索引 | `CREATE INDEX idx_ab ON t (a, b);` |
| 删索引 | `DROP INDEX idx_name ON t;` |
| 查看索引 | `SHOW INDEX FROM t;` |
| 看执行计划 | `EXPLAIN SELECT ...;` |

**最左前缀原则**：联合索引 `(a,b,c)` 能命中 `a` / `a,b` / `a,b,c` 的查询，但单独查 `b` 或 `c` 命中不了。

**索引失效常见场景**：列上用函数/运算（`WHERE YEAR(d)=2024`）、`LIKE '%x'` 前导模糊、隐式类型转换、`OR` 一侧无索引、`!=` / `NOT IN`。

---

## 五、事务

```sql
START TRANSACTION;
UPDATE account SET balance = balance - 100 WHERE id = 1;
UPDATE account SET balance = balance + 100 WHERE id = 2;
COMMIT;        -- 提交；出错则 ROLLBACK 回滚
```

**ACID**：原子性 Atomicity、一致性 Consistency、隔离性 Isolation、持久性 Durability。

**隔离级别**（从低到高，MySQL InnoDB 默认 **可重复读 RR**）：

| 级别 | 脏读 | 不可重复读 | 幻读 |
| --- | --- | --- | --- |
| READ UNCOMMITTED | 可能 | 可能 | 可能 |
| READ COMMITTED | 不会 | 可能 | 可能 |
| **REPEATABLE READ**（默认） | 不会 | 不会 | 基本不会（InnoDB 用 MVCC + 间隙锁解决） |
| SERIALIZABLE | 不会 | 不会 | 不会 |

---

## 六、记忆法（纯对比表）

### 1. 四类语句分类记忆

| 缩写 | 全称 | 管什么 | 代表关键字 |
| --- | --- | --- | --- |
| DDL | Data **Definition** | 结构（库/表/列） | CREATE / ALTER / DROP / TRUNCATE |
| DML | Data **Manipulation** | 数据（行） | INSERT / UPDATE / DELETE |
| DQL | Data **Query** | 查询 | SELECT |
| DCL | Data **Control** | 权限 | GRANT / REVOKE |
| TCL | **Transaction** Control | 事务 | COMMIT / ROLLBACK |

### 2. SQL 书写顺序 vs 执行顺序（最易混，重点记）

| 步骤 | 书写顺序 | **真实执行顺序** |
| --- | --- | --- |
| 1 | SELECT | **FROM**（先确定表） |
| 2 | FROM | **ON / JOIN**（连表） |
| 3 | JOIN | **WHERE**（过滤行） |
| 4 | WHERE | **GROUP BY**（分组） |
| 5 | GROUP BY | **HAVING**（过滤组） |
| 6 | HAVING | **SELECT**（选列） |
| 7 | ORDER BY | **DISTINCT** |
| 8 | LIMIT | **ORDER BY**（排序） |
| 9 | — | **LIMIT**（截断） |

> 记忆钩子：**写在最前的 SELECT，其实倒数第三才执行** → 所以 SELECT 里的列别名不能在 WHERE 用，却能在 ORDER BY 用。

### 3. WHERE vs HAVING

| 维度 | WHERE | HAVING |
| --- | --- | --- |
| 过滤对象 | 原始行 | 分组后的组 |
| 执行时机 | GROUP BY 之前 | GROUP BY 之后 |
| 能用聚合函数 | ✗ | ✓（如 `HAVING COUNT(*)>1`） |

### 4. JOIN 留谁记忆

| JOIN | 一句话 | 留谁 |
| --- | --- | --- |
| INNER | 两边都有才留 | 交集 |
| LEFT | **左**边全留 | 以左为主 |
| RIGHT | **右**边全留 | 以右为主 |

> 钩子：LEFT/RIGHT 看箭头方向——`A LEFT JOIN B`，**LEFT 指 A**，A 全留。

### 5. 三个易错点对比

| 易错 | 错误写法 | 正确写法 |
| --- | --- | --- |
| 判空 | `WHERE col = NULL` | `WHERE col IS NULL` |
| 金额类型 | `FLOAT` / `DOUBLE` | `DECIMAL(10,2)` |
| 去重计数 | `COUNT(DISTINCT col)` 漏 NULL（NULL 不计入，符合预期但需知晓） | 视需求用 `COUNT(*)` |

---

## 相关

- 来源：通用知识整理（建议对照 [MySQL 官方文档](https://dev.mysql.com/doc/)）
