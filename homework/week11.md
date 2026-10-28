# 第 11 周作业：SQLite 与 SQL 基础

> 📖 教程：[SQLite 教程](https://www.runoob.com/sqlite/sqlite-tutorial.html)（建表、INSERT、SELECT、WHERE、ORDER BY、GROUP BY、事务）
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 会建表、增删改查、聚合统计；理解主键、外键、约束、索引。

## 本周安排

| 天 | 学习（约 50 分钟） | 作业（约 2 小时） |
| --- | --- | --- |
| 1 | 安装 DB Browser，认识表/行/列 | 初级 1–2 |
| 2 | `SELECT`、`WHERE`、`ORDER BY`、`LIMIT` | 初级 3 |
| 3 | `INSERT/UPDATE/DELETE`、聚合 | 中级 1–2 |
| 4 | `GROUP BY`、日期函数、子查询 | 中级 3–4 |
| 5 | 主键/外键/约束/索引 | 高级 |
| 6 | 重做 + 笔记 | 复盘 |

## 作业

### 初级（必做，约 35 分钟）

1. 安装 [DB Browser for SQLite](https://sqlitebrowser.org/)，新建 `code/week11/test.db`。
2. 建表并插入 5 条数据：
   ```sql
   CREATE TABLE students (
       id    INTEGER PRIMARY KEY AUTOINCREMENT,
       name  TEXT NOT NULL,
       age   INTEGER,
       score REAL
   );

   INSERT INTO students (name, age, score) VALUES
       ('小明', 18, 88.5),
       ('小红', 17, 92.0),
       ('小刚', 18, 76.5),
       ('小美', 19, 95.0),
       ('小强', 17, 59.0);
   ```
3. 在“执行 SQL”里依次运行并截图/记录结果：
   - 查询全部；
   - 只查姓名和分数；
   - 分数 ≥ 80 的人；
   - 按分数从高到低排序；
   - 前 3 名；
   - 年龄等于 18 且分数大于 80 的人。

**验收**：能解释 `WHERE`、`ORDER BY`、`LIMIT` 的顺序；知道 `NULL` 和 0 不是一回事。

### 中级（必做，约 70 分钟）

在 `test.db` 中建记账相关表并练习：

```sql
CREATE TABLE categories (
    id   INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL UNIQUE,
    kind TEXT NOT NULL
);

CREATE TABLE records (
    id          INTEGER PRIMARY KEY AUTOINCREMENT,
    date        TEXT NOT NULL,
    kind        TEXT NOT NULL,
    category_id INTEGER NOT NULL,
    amount      REAL NOT NULL,
    note        TEXT
);
```

插入 7 个分类（餐饮、交通、购物、工资、兼职等）和 12 条记录（覆盖 2026-09 和 2026-10 两个月，收支都有）。

写 `sql/week11.sql`，至少包含 10 条查询，每条上面用 `--` 注释说明目的：

1. 查所有记录，带上分类名（`JOIN`）；
2. 查 2026 年 10 月的记录；
3. 查支出金额大于 100 的记录；
4. 按金额降序，取前 5；
5. 算 2026-10 的收入合计、支出合计；
6. 按分类统计 2026-10 的支出，从高到低；
7. 统计每个分类的记录条数；
8. 查没有备注的记录；
9. 把某条记录的金额加 10；
10. 删除 2026-09 的某一条测试记录；
11. （选做）按月份统计收支；
12. （选做）找出金额高于全部记录平均值的记录。

**验收**：每条 SQL 都能独立运行；`JOIN` 不丢行、不重复行；能解释 `GROUP BY` 和 `SUM` 的配合。

### 高级（挑战，约 50 分钟）

为毕业项目设计最终数据库：

1. 参考 [PROJECT.md](../PROJECT.md) 的 schema，自己写 `sql/schema.sql`，要求：
   - `categories` 和 `records` 两张表；
   - `kind` 只能是 `income` 或 `expense`（`CHECK`）；
   - `amount` 必须大于 0；
   - `category_id` 外键引用 `categories(id)`；
   - `date`、`category_id` 建索引；
   - 开启 `PRAGMA foreign_keys = ON;`。
2. 在 DB Browser 里执行，插入初始分类；故意插入一条 `amount = -1` 和一条不存在的 `category_id`，记录报错信息（验证约束生效）。
3. 在笔记里回答：
   - 为什么金额用整数“分”而不是小数？
   - 索引加快了什么操作？会拖慢什么？
   - 删除一个已被记录引用的分类，应该怎么处理？
4. 写 3 条你项目要用的查询：某月列表、某月合计、某月分类汇总。

**验收**：约束真的能拦住脏数据；能说出主键和外键各自的作用；`schema.sql` 可以在空库上一键执行。

## 提交

- 数据库：`code/week11/test.db` 不要提交（`.gitignore` 已忽略 `*.db`）
- SQL：`sql/week11.sql`、`sql/schema.sql`
- 笔记：`notes/week11.md`（约束报错、索引、金额单位）
- 进度：PROGRESS.md 第 11 行
- Git：`week11: 完成 SQL 练习和项目 schema`

## 自检

- [ ] 我知道 `SELECT` 的执行顺序大致是 `FROM → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT`。
- [ ] 我知道 `WHERE` 过滤行，`HAVING` 过滤分组。
- [ ] 我知道主键唯一且非空，外键保证引用存在。
- [ ] 我知道字符串日期 `YYYY-MM-DD` 可以直接比较大小、可以用 `substr` 取月份。
- [ ] 我不会把真实账目数据库提交到 GitHub。
