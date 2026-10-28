# 第 12 周作业：Python 操作 SQLite

> 📖 文档：[sqlite3 官方文档](https://docs.python.org/zh-cn/3/library/sqlite3.html)
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 会用 Python 连接数据库、参数化查询、事务提交；会封装 DAO；知道怎么防 SQL 注入。

## 本周安排

| 天 | 学习（约 50 分钟） | 作业（约 2 小时） |
| --- | --- | --- |
| 1 | `connect/cursor/execute/fetch` | 初级 1–2 |
| 2 | `commit`、`with conn`、`Row` | 初级 3 |
| 3 | 参数化查询、增删改查封装 | 中级 1–2 |
| 4 | 事务、异常回滚、备份 | 中级 3 |
| 5 | 导入 CSV、防注入 | 高级 |
| 6 | 重做 + 笔记 | 复盘 |

## 作业

### 初级（必做，约 35 分钟）

`db_basic.py`：

1. 连接 `code/week12/demo.db`（不存在会自动创建）；
2. 建表 `notes(id INTEGER PRIMARY KEY AUTOINCREMENT, title TEXT, body TEXT, created_at TEXT)`；
3. 插入 2 条笔记，用 `with conn:` 提交；
4. 查询全部并打印，要求打印成 `id | title | created_at`；
5. 用 `conn.row_factory = sqlite3.Row` 再查一次，用列名取值；
6. 更新一条、删除一条，再查询确认；
7. 最后 `conn.close()`。

**验收**：重复运行不报“表已存在”；中文正常；知道 `commit()` 不调用会怎样。

### 中级（必做，约 70 分钟）

`record_dao.py`：实现记账项目的 `RecordDAO`：

```python
class RecordDAO:
    def __init__(self, db_path): ...
    def add(self, date, kind, category_id, amount, note=""): ...
    def get(self, record_id): ...
    def list_by_month(self, month): ...        # month = "2026-10"
    def update(self, record_id, **fields): ...
    def delete(self, record_id): ...
    def search(self, keyword): ...
    def month_summary(self, month): ...        # 返回 {"income": ..., "expense": ...}
```

要求：

- **全部使用 `?` 参数化查询**，禁止 f-string 拼 SQL；
- `amount` 以“分”为单位存整数，提供 `yuan_to_fen` / `fen_to_yuan` 两个函数并测试；
- 所有方法自己管理连接，异常时回滚并关闭；
- 写 `seed.py` 插入 30 条测试数据（分布在不同月份和分类）；
- 写 8 条调用示例，打印结果。

**验收**：`list_by_month("2026-10")` 只返回该月；`search("午饭")` 能查到备注；金额 25.00 元存成 2500，显示回 25.00。

### 高级（挑战，约 50 分钟）

1. **CSV 导入 + 事务**：写 `import_csv.py`，读取 `samples/records.csv`（自己造 20 行），逐行插入：
   - 任何一行格式错误（日期错、金额 ≤ 0、分类不存在）→ 整批回滚，打印第几行出错；
   - 全部成功才提交，并打印导入条数。
2. **备份与恢复**：用 `source.backup(target)` 把数据库备份到 `backup/expense_YYYYMMDD_HHMMSS.db`；写一个恢复函数（复制回来前先关闭连接）。
3. **防注入演示**：写两段代码查记录：
   - 错误写法：`f"SELECT * FROM records WHERE note LIKE '%{kw}%'"`，输入 `' OR 1=1 --` 观察结果；
   - 正确写法：`... WHERE note LIKE ?`，参数 `f"%{kw}%"`，观察结果。
   
   把两次结果和原因写进笔记。
4. 给第 13 周的 CLI 版画一个模块图：`db.py`、`service.py`、`cli.py` 各自负责什么，谁调用谁。

**验收**：错误 CSV 一行都不入库；备份文件能打开且数据完整；能解释参数化为什么能防注入。

## 提交

- 代码：`code/week12/db_basic.py`、`record_dao.py`、`seed.py`、`import_csv.py`
- 示例：`samples/records.csv`（虚构数据）
- 笔记：`notes/week12.md`（防注入对比、事务回滚、金额单位）
- 进度：PROGRESS.md 第 12 行
- Git：`week12: 完成 RecordDAO 和导入备份`

## 自检

- [ ] 我的 SQL 里没有用 `+` 或 f-string 拼用户输入。
- [ ] 我知道 `with conn:` 管的是事务，不是关闭连接。
- [ ] 我知道 `fetchone()` / `fetchall()` 的区别。
- [ ] 我知道数据库文件不要提交，示例数据用 `samples/`。
- [ ] 我的金额换算函数有测试，25.00 ↔ 2500 不会错。
