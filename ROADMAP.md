# 18 周详细路线

配套教材：[菜鸟教程 Python 3](https://www.runoob.com/python3/python3-tutorial.html)。每周 6 天 × 3 小时，第 7 天复盘。作业在 `homework/weekXX.md`。

图例：📖 教程章节 · 🎯 本周目标 · 📦 本周产出 · ✅ 验收（做到才算过）

---

## 第一阶段：语法入门（第 1–4 周）

### 第 1 周 · 环境与第一批程序

- 📖 简介、环境搭建、VS Code、基础语法、基本数据类型、数据类型转换、注释、运算符、数字、输入输出
- 🎯 装好环境；理解“文件 → 解释器 → 输出”；会定义变量、做四则运算、用 `input()` 和 `print()`。
- 📦 `hello.py`、`profile.py`、`bill.py`
- ✅ 能在终端用 `python 文件名.py` 运行；能解释 `int` / `float` / `str` 的区别；变量名见名知意。

### 第 2 周 · 字符串与数字

- 📖 字符串、数字、运算符（补充）
- 🎯 索引、切片、常用字符串方法、f-string 格式化、保留小数、类型转换。
- 📦 `text_stats.py`、`template.py`
- ✅ 切片不越界；能说出 `strip` / `split` / `join` / `replace` 各自做什么；金额输出两位小数。

### 第 3 周 · 列表、元组、集合与 for 循环

- 📖 列表、元组、集合、循环语句（`for` 部分）
- 🎯 增删改查、排序、切片、`for` 遍历；理解可变与不可变；用集合去重和做交并差。
- 📦 `scores.py`、`todo.py`、`names.py`
- ✅ 能用 `for` + `enumerate` 遍历列表；知道什么时候用列表、什么时候用集合。

### 第 4 周 · 字典、条件与 while 循环

- 📖 字典、条件控制、循环语句
- 🎯 用字典描述一条记录；`if/elif/else`；`while` / `break` / `continue`；嵌套字典。
- 📦 `contacts_v0.py`、`students.py`、`guess_number.py`
- ✅ 能遍历字典的键/值/键值对；能写带退出条件的循环菜单；嵌套数据取值不报 `KeyError`。

---

## 第二阶段：函数与数据（第 5–8 周）

### 第 5 周 · 函数与推导式

- 📖 函数、lambda、推导式、迭代器与生成器（入门）
- 🎯 参数、返回值、默认参数、作用域；列表/字典推导式；`sorted(key=...)`；生成器概念。
- 📦 `utils.py`、`tools_test.py`
- ✅ 一个函数只做一件事；能解释“可变默认参数”的坑；能写简单的推导式。

### 第 6 周 · 模块与标准库

- 📖 模块、`__name__`、标准库概览、日期和时间、random、math
- 🎯 拆分模块、`import`、包、`if __name__ == "__main__"`；常用标准库。
- 📦 多模块版通讯录 `address_book/`
- ✅ 模块能互相导入；主程序不再堆在一个文件里；知道去哪查标准库。

### 第 7 周 · 文件、CSV/JSON、异常

- 📖 输入输出、File、OS、with、错误和异常、JSON、CSV（`csv` 模块）
- 🎯 `pathlib`、文本读写、编码、CSV/JSON 存取、`try/except/else/finally`。
- 📦 通讯录 v1（可保存到文件）
- ✅ 中文不乱码；文件不存在不崩溃；`with open` 使用正确。

### 第 8 周 · 面向对象

- 📖 面向对象、命名空间/作用域、类型注解
- 🎯 类、对象、`__init__`、实例属性/方法、封装、继承（了解）、`dataclass`。
- 📦 通讯录 v2（OOP 重构）
- ✅ 能解释 `self` 和实例属性；数据与操作封装进类；代码比 v1 更清晰。

---

## 第三阶段：工程与数据库（第 9–13 周）

### 第 9 周 · venv 与 Git

- 📖 虚拟环境的创建、pip；[Git 教程](https://www.runoob.com/git/git-tutorial.html)
- 🎯 创建/激活 venv、`pip install`、`requirements.txt`；Git 四区、提交、回滚、远程仓库。
- 📦 带 `.venv` 和 `.gitignore` 的项目；`docs/git-cheatsheet.md`
- ✅ 能独立从零建环境；能说清工作区/暂存区/本地/远程；提交信息有意义。

### 第 10 周 · 工程化：结构、日志、测试

- 📖 模块/包（复习）、错误和异常（复习）；pytest 官方文档
- 🎯 包结构、入口文件、logging、断点调试、pytest 基础。
- 📦 通讯录 v3：`app/` 包 + 日志 + 5 个测试
- ✅ `pytest -q` 全绿；日志有时间和级别；能用断点找到 bug。

### 第 11 周 · SQLite 与 SQL 基础

- 📖 [SQLite 教程](https://www.runoob.com/sqlite/sqlite-tutorial.html)
- 🎯 建表、主键、增删改查、`WHERE` / `ORDER BY` / `LIMIT`、聚合与分组、外键、索引。
- 📦 `sql/week11.sql`、记账本 `schema.sql`
- ✅ 能独立写出 CRUD 和月度/分类统计 SQL；理解主键、外键、索引。

### 第 12 周 · Python 操作 SQLite

- 📖 [sqlite3 官方文档](https://docs.python.org/zh-cn/3/library/sqlite3.html)
- 🎯 `connect` / `cursor` / `commit` / `close`、参数化查询、事务、`Row`、备份。
- 📦 `db.py` + `RecordDAO` + 测试数据
- ✅ 全程参数化查询；异常时连接能关闭；中文读写正常。

### 第 13 周 · 数据层完成 + 命令行记账本（里程碑 M1）

- 📖 复习：函数、异常、SQL、日志、测试
- 🎯 统计查询、输入校验、CSV 导出、分层（db / service / cli）。
- 📦 命令行记账本 v0.9，可增删查、月统计、导出
- ✅ 空数据库开始能完整走通；重启数据不丢；核心函数有测试。

---

## 第四阶段：界面与交付（第 14–18 周）

### 第 14 周 · Tkinter 基础

- 📖 [Tkinter 教程](https://www.runoob.com/python/python-gui-tkinter.html)、[官方 tkinter 文档](https://docs.python.org/zh-cn/3/library/tkinter.html)
- 🎯 窗口、`Label` / `Button` / `Entry`、`pack` / `grid`、事件绑定、`messagebox`。
- 📦 登录表单、单位换算器
- ✅ 布局不重叠；按钮能触发函数；空输入有提示。

### 第 15 周 · Tkinter 进阶

- 📖 ttk、`Treeview`、`Combobox`、变量类、菜单、对话框
- 🎯 表格展示、选中行、菜单栏、多 Frame 切换、样式。
- 📦 记账界面原型（假数据）
- ✅ 表格能刷新；切换页面不重复开窗；能取到选中行。

### 第 16 周 · 整合 GUI 与数据库（里程碑 M2）

- 📖 复习：Tkinter + sqlite3
- 🎯 表单写入数据库、表格读取、修改/删除、筛选、统计页。
- 📦 小账本 GUI 可用版
- ✅ 完整增删改查；与 CLI 共用同一个数据库；没有未捕获异常。

### 第 17 周 · 打磨与用户测试（里程碑 M3）

- 📖 复习：异常、文件、CSV、日志
- 🎯 输入校验、二次确认、搜索筛选、CSV 导出、备份、空状态、快捷键。
- 📦 小账本 v0.9.5 + 使用说明初稿
- ✅ 连续操作 10 分钟不崩；异常有友好提示；别人能按文档跑起来。

### 第 18 周 · 打包与发布（里程碑 M4）

- 📖 [PyInstaller 文档](https://pyinstaller.org/en/stable/)
- 🎯 `--onefile` / `--windowed` / `--icon`、打包后路径问题、Release 流程。
- 📦 小账本 v1.0：exe + README + CHANGELOG + tag
- ✅ 新目录双击 exe 可用且能保存数据；GitHub Release 已上传；能 3 分钟演示。

---

## 毕业之后（选学，不占 18 周）

按兴趣挑，不要一次全学：

- 正则表达式、`requests` + 接口、多线程/异步（菜鸟教程高级部分）
- pandas / Excel 自动化、matplotlib 图表
- Web：Flask / FastAPI；自动化：selenium / playwright
- 测试进阶：pytest 夹具、覆盖率；CI（GitHub Actions）
- 代码质量：ruff / black、类型检查 mypy
