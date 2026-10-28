# 第 4 周作业：字典、条件、循环

> 📖 教程：[字典](https://www.runoob.com/python3/python3-dictionary.html) · [条件控制](https://www.runoob.com/python3/python3-conditional-statements.html) · [循环语句](https://www.runoob.com/python3/python3-loop.html)
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 用字典描述一条记录；会写 `if/elif/else`；会用 `while` 写菜单，用 `for` 处理多条数据。

## 本周安排

| 天 | 学习（约 50 分钟） | 作业（约 2 小时） |
| --- | --- | --- |
| 1 | 字典增删改查、遍历 | 初级 1 |
| 2 | 条件判断、成绩等级 | 初级 2 |
| 3 | `while`、`break`、`continue` | 中级 |
| 4 | 嵌套字典、菜单整合 | 中级收尾 |
| 5 | 挑战题 | 高级 |
| 6 | 重做 + 笔记 | 复盘 |

## 作业

### 初级（必做，约 35 分钟）

1. `contacts.py`：用字典保存一个联系人：
   ```python
   contact = {"name": "小明", "phone": "13800000000", "city": "杭州"}
   ```
   - 输出姓名和电话；
   - 新增 `"email"`，修改 `"city"`，删除 `"phone"`；
   - 分别遍历输出所有键、所有值、所有键值对；
   - 用 `get("address", "未填写")` 取值，观察和 `contact["address"]` 的区别（把报错记下来）。
2. `grade.py`：输入 0–100 的分数，输出等级：90+ 为 A，80–89 为 B，70–79 为 C，60–69 为 D，低于 60 为 E。
   - 先写 `if/elif/else`；
   - 再故意输入 `101` 和 `-1`，思考应该怎么处理（这周先输出“分数不合法”即可）。

**验收**：能解释 `[]` 和 `get()` 取不到键时的区别；条件顺序不会写反。

### 中级（必做，约 70 分钟）

`students.py`：内存版学生成绩管理，用**嵌套字典**：

```python
students = {
    "小明": {"chinese": 88, "math": 95, "english": 90},
    "小红": {"chinese": 92, "math": 78, "english": 85},
}
```

用 `while True` 写菜单：

```
1. 添加学生  2. 查看全部  3. 查询学生  4. 统计  5. 退出
```

- 添加：输入姓名和三科成绩，写入字典；
- 查看：遍历输出每人三科和总分；
- 查询：输入姓名，输出各科成绩；不存在时提示；
- 统计：输出班级人数、每科平均分、总分最高的人；
- 退出：`break`；
- 输入非 1–5 时提示“请输入 1-5”。

**提示**：总分排序可以用 `sorted(students.items(), key=lambda kv: sum(kv[1].values()), reverse=True)`，lambda 下周正式学，先照抄并写一句理解。

**验收**：连续操作 1→2→3→4→5 不崩；查询不存在的学生有提示；平均分保留 2 位。

### 高级（挑战，约 45 分钟，二选一，都做加分）

**A. 猜数字** `guess_number.py`：

- 程序随机 1–100 的整数（`import random`，`random.randint(1, 100)`）；
- 最多猜 7 次，每次提示“太大/太小/猜对”；
- 用完次数提示正确答案；
- 结束后问“再来一局？(y/n)”，`y` 重新开始，`n` 退出。

**B. 模拟 ATM** `atm.py`：

- 初始余额 1000；
- 菜单：查询 / 存款 / 取款 / 退出；
- 存款、取款金额必须 > 0；取款不能超过余额；
- 每次操作后显示最新余额；
- 输入 `q` 退出。

**验收**：循环有明确退出条件；所有分支都实际跑过一遍；非法金额不会把余额变负。

## 提交

- 代码：`code/week04/contacts.py`、`grade.py`、`students.py`、`guess_number.py` 或 `atm.py`
- 笔记：`notes/week04.md`（`[]` vs `get`、`break` vs `continue`、字典嵌套怎么取值）
- 进度：PROGRESS.md 第 4 行
- Git：`week04: 完成初级和中级`

## 自检

- [ ] 我能写出 `for key, value in d.items()`。
- [ ] 我知道 `while True` 必须配 `break` 或明确条件。
- [ ] 我知道 `if` 的判断顺序会影响结果（先判 90 再判 80）。
- [ ] 嵌套字典取值写成 `students[name]["math"]`，不写成 `students[name["math"]]`。
- [ ] 菜单程序每个选项我都实际点过。
