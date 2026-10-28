# 毕业项目：小账本（ExpenseLite）

> 这是第 13–18 周的项目规格。第 13 周先做命令行版，第 14 周起换图形界面，最后打包发布。
> 不要一开始就写 GUI：**先把数据层和业务逻辑写对，界面只是外壳。**

## 1. 产品一句话

一个给自己用的 Windows 桌面记账小工具：记下每天的收支，按月看统计，能导出 CSV，双击 exe 就能用，数据存在本地 SQLite。

## 2. 目标用户与场景

- 用户：你自己（单用户、单机、不需要登录）。
- 场景：每天花 1 分钟记 2–5 笔账；月底看本月支出和分类占比；换电脑时能备份/导出。
- 不做什么（明确非目标）：多用户、云同步、联网、手机端、复杂图表、导入银行账单。

## 3. 功能清单

### P0（v1.0 必须有）

- [ ] 新增记录：日期、类型（收入/支出）、分类、金额、备注。
- [ ] 记录列表：按日期倒序显示，支持选中。
- [ ] 修改记录、删除记录（删除要二次确认）。
- [ ] 按月筛选（如 2026-10）。
- [ ] 统计：本月收入、支出、结余；按分类汇总支出。
- [ ] 输入校验：金额 > 0、日期格式正确、分类必选。
- [ ] 数据持久化：关闭程序再打开，数据还在。
- [ ] 导出 CSV（带表头，Excel 打开中文不乱码）。
- [ ] 打包成 exe，新目录双击可运行。

### P1（有余力再做）

- [ ] 关键词搜索备注/分类。
- [ ] 一键备份数据库到指定目录。
- [ ] 分类管理（新增/停用分类）。
- [ ] 关于窗口、版本号、图标。
- [ ] 快捷键（Ctrl+N 新增、Delete 删除、F5 刷新）。

### P2（毕业后再做）

- [ ] 月度趋势图（matplotlib 或 tkinter Canvas）。
- [ ] 预算与超支提醒。
- [ ] 多账本/多币种。

## 4. 数据库设计

金额用**整数分**存储，避免浮点误差（1 元 = 100 分）。界面上显示元，存取时转换。

```sql
PRAGMA foreign_keys = ON;

CREATE TABLE IF NOT EXISTS categories (
    id      INTEGER PRIMARY KEY AUTOINCREMENT,
    name    TEXT    NOT NULL UNIQUE,
    kind    TEXT    NOT NULL CHECK (kind IN ('income', 'expense')),
    active  INTEGER NOT NULL DEFAULT 1
);

CREATE TABLE IF NOT EXISTS records (
    id          INTEGER PRIMARY KEY AUTOINCREMENT,
    date        TEXT    NOT NULL,              -- YYYY-MM-DD
    kind        TEXT    NOT NULL CHECK (kind IN ('income', 'expense')),
    category_id INTEGER NOT NULL REFERENCES categories(id),
    amount      INTEGER NOT NULL CHECK (amount > 0),  -- 单位：分
    note        TEXT    NOT NULL DEFAULT '',
    created_at  TEXT    NOT NULL DEFAULT (datetime('now', 'localtime'))
);

CREATE INDEX IF NOT EXISTS idx_records_date ON records(date);
CREATE INDEX IF NOT EXISTS idx_records_category ON records(category_id);
```

初始分类（可改）：

- 支出：餐饮、交通、购物、居住、学习、医疗、其他
- 收入：工资、兼职、红包、其他

常用查询：

```sql
-- 某月全部记录
SELECT r.id, r.date, r.kind, c.name AS category, r.amount, r.note
FROM records r JOIN categories c ON c.id = r.category_id
WHERE substr(r.date, 1, 7) = ?          -- '2026-10'
ORDER BY r.date DESC, r.id DESC;

-- 某月收支合计
SELECT kind, SUM(amount) FROM records
WHERE substr(date, 1, 7) = ? GROUP BY kind;

-- 某月支出分类汇总
SELECT c.name, SUM(r.amount)
FROM records r JOIN categories c ON c.id = r.category_id
WHERE substr(r.date, 1, 7) = ? AND r.kind = 'expense'
GROUP BY c.name ORDER BY SUM(r.amount) DESC;

-- 删除分类前检查是否被引用
SELECT COUNT(*) FROM records WHERE category_id = ?;
```

## 5. 界面草图

```
┌─ 小账本 v1.0 ────────────────────────────────────────────┐
│ [记账] [统计]                              [备份] [关于] │
├──────────────────────────────────────────────────────────┤
│ 月份: [2026-10 ▼]  类型: [全部 ▼]  搜索: [______] [查询] │
│                                                          │
│  日期        类型   分类    金额(元)   备注               │
│  2026-10-28  支出   餐饮     25.00     午饭               │
│  2026-10-28  收入   工资   8000.00     10月工资           │
│  ...                                                     │
│                                                          │
├──────────────────────────────────────────────────────────┤
│ 日期[2026-10-28] 类型[支出▼] 分类[餐饮▼] 金额[25.00]     │
│ 备注[午饭__________________]  [新增] [保存修改] [删除]   │
├──────────────────────────────────────────────────────────┤
│ 本月收入 8000.00   本月支出 1250.00   结余 6750.00       │
└──────────────────────────────────────────────────────────┘
```

统计页：上方三个数字卡片，中间分类汇总表（分类 / 金额 / 占比），下方“导出 CSV”。

## 6. 目录结构（建议）

```
project/
├── main.py                 # 入口：初始化数据库，启动窗口
├── app/
│   ├── __init__.py
│   ├── config.py           # 路径、常量、版本号
│   ├── db.py               # 连接、建表、初始化分类
│   ├── models.py           # Record / Category（dataclass）
│   ├── service.py          # 业务逻辑：增删改查、统计、导出
│   └── ui/
│       ├── __init__.py
│       ├── main_window.py  # 主窗口、切换页
│       ├── record_view.py  # 记账页
│       └── stats_view.py   # 统计页
├── sql/schema.sql          # 建表语句（与 db.py 保持一致）
├── tests/test_service.py   # pytest
├── assets/icon.ico
├── requirements.txt
├── README.md               # 安装、使用、截图、FAQ
└── CHANGELOG.md
```

第 13 周可以先简化为 `db.py` / `service.py` / `cli.py` / `main.py`，第 16 周再拆 `ui/`。

## 7. 数据文件放在哪

- 开发时：项目目录下 `data/expense.db`（加入 `.gitignore`，不要提交真实账目）。
- 打包后：写到 `%APPDATA%\ExpenseLite\expense.db`，不要写进 exe 所在目录（可能没有写权限，且升级会丢）。
- 用 `pathlib.Path(os.getenv("APPDATA")) / "ExpenseLite"` 拼路径，目录不存在就 `mkdir`。

## 8. 里程碑

| 里程碑 | 时间 | 交付物 | 过关标准 |
| --- | --- | --- | --- |
| M1 数据层 + CLI | 第 13 周 | 命令行记账本 v0.9 | 空库开始能增删查、月统计、导出 CSV |
| M2 GUI 可用 | 第 16 周 | 图形界面版 | 增删改查全通，和 CLI 共用同一个库 |
| M3 打磨完成 | 第 17 周 | v0.9.5 | 有校验、确认、搜索、备份、使用说明 |
| M4 正式发布 | 第 18 周 | v1.0.0 + exe | 新目录双击可用，Release 和 tag 建好 |

## 9. 手工验收用例（发布前逐条做）

1. 全新环境启动，自动建库、自动写入初始分类，不报错。
2. 新增一笔支出 25.00，列表出现，金额显示 25.00。
3. 新增一笔收入 8000.00，月统计收入/支出/结余正确。
4. 修改刚才的支出为 30.00，列表和统计同步更新。
5. 删除记录，弹出确认；取消不删，确认才删。
6. 金额输入 `0`、`-5`、`abc`、空，均有提示且不写库。
7. 日期输入 `2026-13-40` 有提示。
8. 切换到没有数据的月份，显示空状态而不是报错。
9. 导出 CSV，用 Excel 打开中文正常，金额与界面一致。
10. 关闭程序再打开，数据仍在；备份后删库，用备份能恢复。
11. 把 `dist/` 里的 exe 复制到新文件夹，双击能启动并新增记录。
12. 断网、路径含中文/空格，程序仍能启动。

## 10. 评分（自己打，诚实一点）

| 维度 | 分值 | 说明 |
| --- | --- | --- |
| 功能完整 | 30 | P0 全部完成 |
| 数据正确 | 20 | 金额、统计、持久化无错 |
| 健壮性 | 15 | 非法输入、异常路径不崩 |
| 代码结构 | 15 | 分层清晰、命名合理、无大段复制 |
| 界面可用 | 10 | 布局整齐、操作顺手 |
| 交付文档 | 10 | README 能让他人独立运行 |

80 分以上算毕业；不到就按低分项补，不新增功能。
