# 第 6 周作业：模块与标准库

> 📖 教程：[模块](https://www.runoob.com/python3/python3-module.html) · [标准库概览](https://www.runoob.com/python3/python3-stdlib.html) · [日期和时间](https://www.runoob.com/python3/python3-date-time.html)
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 会把代码拆成多个文件；理解 `import` 和 `__name__`；会用 `datetime`、`random`、`math`、`collections`。

## 本周安排

| 天 | 学习（约 50 分钟） | 作业（约 2 小时） |
| --- | --- | --- |
| 1 | 模块、`import`、`__name__` | 初级 |
| 2 | 包、`from ... import`、标准库巡览 | 初级收尾 |
| 3 | `datetime`、`random`、`math` | 中级 1–2 |
| 4 | `collections`、综合 | 中级 3–4 |
| 5 | 挑战题 | 高级 |
| 6 | 重做 + 笔记 | 复盘 |

## 作业

### 初级（必做，约 35 分钟）

1. 把第 5 周的 `utils.py` 整理成模块，目录：
   ```
   code/week06/
   ├── main.py
   └── mytools/
       ├── __init__.py
       └── utils.py
   ```
   在 `main.py` 里用 `from mytools.utils import is_prime, format_money` 调用，确认能运行。
2. 在 `utils.py` 末尾加：
   ```python
   if __name__ == "__main__":
       print(is_prime(7))       # 自测
       print(format_money(1234.5))
   ```
   分别运行 `python mytools/utils.py` 和 `python main.py`，观察自测代码什么时候执行，把结论写进笔记。
3. 用 `import this` 看一眼 Python 之禅，挑一条你觉得最重要的抄进笔记。

**验收**：`main.py` 能导入并使用函数；能解释 `__name__ == "__main__"` 的作用。

### 中级（必做，约 70 分钟）

写 `stdlib_demo.py`，每个功能一个函数：

1. `days_until(target)`：输入 `"2027-01-01"`，返回距今天还有多少天（用 `datetime.date`）。再算一下你今年的年龄。
2. `make_code(length=6)`：生成由数字和大写字母组成的随机验证码。
3. `circle_area(r)`：用 `math.pi` 算圆面积，保留 2 位；再算 `math.sqrt(2)`。
4. `word_count(text)`：用 `collections.Counter` 统计单词频率，输出出现最多的 3 个。
5. `group_by_first_letter(words)`：用 `collections.defaultdict(list)` 按首字母分组。
6. 用 `random.choice` 从名单里抽 3 个人（不重复，用 `random.sample`）。

每个函数在 `if __name__ == "__main__":` 里跑一遍示例。

**验收**：日期计算不受月份天数影响；验证码每次不同；能说出 `Counter` 和普通字典的区别。

### 高级（挑战，约 50 分钟）

`address_book/`：多模块版通讯录 v0（**先不存文件**，数据在内存，程序退出就没了，第 7 周再加保存）。

目录建议：

```
code/week06/address_book/
├── main.py          # 菜单和输入输出
├── contacts.py      # 数据操作：add/list/search/delete
└── __init__.py
```

功能：

- 菜单：添加 / 列表 / 搜索 / 删除 / 退出；
- 联系人用字典：`{"name": ..., "phone": ..., "city": ...}`；
- 用列表保存多个联系人；
- 搜索支持姓名包含关键字（不区分大小写）；
- 删除按姓名精确匹配，找不到给提示；
- 菜单逻辑放 `main.py`，数据操作放 `contacts.py`，`main.py` 里不出现复杂的数据处理。

**验收**：连续添加 3 人→搜索→删除→列表→退出，全程不崩；`contacts.py` 能单独导入测试。

## 提交

- 代码：`code/week06/mytools/`、`main.py`、`stdlib_demo.py`、`address_book/`
- 笔记：`notes/week06.md`（`__main__` 结论、Python 之禅一条、`Counter` 用法）
- 进度：PROGRESS.md 第 6 行
- Git：`week06: 完成初级和中级`

## 自检

- [ ] 我知道 `import utils` 和 `from utils import is_prime` 的区别。
- [ ] 我知道包目录里要有 `__init__.py`（3.3+ 可以没有，但先养成习惯）。
- [ ] 我遇到不会的函数会去查官方文档，而不是凭感觉猜。
- [ ] 我的模块名不和标准库重名（不叫 `random.py`、`json.py`）。
- [ ] 我知道 `datetime` 是模块，`date`/`datetime` 是里面的类。
