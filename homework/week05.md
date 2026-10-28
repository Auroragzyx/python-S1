# 第 5 周作业：函数与推导式

> 📖 教程：[函数](https://www.runoob.com/python3/python3-function.html) · [lambda](https://www.runoob.com/python3/python-lambda.html) · [推导式](https://www.runoob.com/python3/python-comprehension.html) · [迭代器与生成器](https://www.runoob.com/python3/python3-iterator-generator.html)
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 会把重复代码抽成函数；理解参数/返回值/作用域；会写简单的推导式和生成器。

## 本周安排

| 天 | 学习（约 50 分钟） | 作业（约 2 小时） |
| --- | --- | --- |
| 1 | 函数定义、参数、返回值 | 初级 |
| 2 | 默认参数、关键字参数、作用域 | 初级重写 |
| 3 | 列表/字典推导式、`sorted(key=)` | 中级 1–3 |
| 4 | lambda、生成器概念 | 中级 4–5 |
| 5 | 挑战题 | 高级 |
| 6 | 重做 + 笔记 | 复盘 |

## 作业

### 初级（必做，约 35 分钟）

把第 4 周的 `students.py` 改写成 `students_func.py`，至少拆出：

- `add_student(students, name, chinese, math, english)`：添加并返回字典；
- `student_total(scores)`：返回三科总分；
- `class_average(students, subject)`：返回某科平均分；
- `top_student(students)`：返回总分最高的人名。

要求：

1. 每个函数有 docstring（一句话说明参数和返回值）；
2. 主程序只负责输入输出和调用函数；
3. 函数里**不要**写 `input()` 和 `print()`（`top_student` 返回名字，由主程序打印）。

**验收**：每个函数单独调用一次能看到正确结果；主程序比原版短、更好读。

### 中级（必做，约 70 分钟）

新建 `utils.py`，实现 5 个函数，并写 `tools_test.py` 调用测试：

1. `is_prime(n)`：判断质数，返回 `True/False`；
2. `fib_list(n)`：返回斐波那契前 n 项的列表（`n=6` → `[1, 1, 2, 3, 5, 8]`）；
3. `dedupe(items)`：列表去重且保留原顺序；
4. `count_vowels(text)`：统计元音个数，大小写都算；
5. `format_money(amount)`：返回 `"¥1,234.50"` 这种格式（千分位 + 两位小数）。

另外在 `tools_test.py` 里用**列表推导式**输出：

- 1–100 中所有偶数的平方；
- 给定单词列表，取出长度 ≥ 4 的单词并转大写；
- 用字典推导式把 `["a", "b", "c"]` 变成 `{"a": 1, "b": 2, "c": 3}`。

每个函数至少测 3 组数据（正常、边界、异常输入）。`is_prime(1)`、`is_prime(2)`、`dedupe([])` 这些边界必须测。

**验收**：`format_money(0)` 得到 `¥0.00`，`format_money(1234.5)` 得到 `¥1,234.50`；`fib_list(1)` 不报错。

### 高级（挑战，约 45 分钟）

1. **生成器** `gen.py`：
   - `fib_gen(n)`：用 `yield` 逐个产生斐波那契数，用 `for` 打印前 10 个；
   - `read_in_chunks(text, size)`：把长字符串按每 `size` 个字符分批 `yield`，模拟分批读文件。
2. **多字段排序**：给定学生列表
   ```python
   students = [
       {"name": "小明", "score": 90, "age": 18},
       {"name": "小红", "score": 90, "age": 17},
       {"name": "小刚", "score": 85, "age": 18},
   ]
   ```
   先按分数降序，分数相同按年龄升序，输出姓名。用 `sorted(..., key=lambda s: (-s["score"], s["age"]))`。
3. 在笔记里用自己的话回答：
   - 列表推导式和 `for` 循环相比，什么时候更好读？
   - 生成器和列表的区别是什么？为什么生成器省内存？
   - 下面这段为什么每次调用都“记住了”上一次的元素？
     ```python
     def add(item, bucket=[]):
         bucket.append(item)
         return bucket
     ```
     正确写法是什么？

**验收**：能解释 `yield` 暂停/恢复；能说出可变默认参数的正确写法 `bucket=None`。

## 提交

- 代码：`code/week05/students_func.py`、`utils.py`、`tools_test.py`、`gen.py`
- 笔记：`notes/week05.md`（3 个问题的回答 + 函数拆分前后对比）
- 进度：PROGRESS.md 第 5 行
- Git：`week05: 完成初级和中级`

## 自检

- [ ] 我的函数名是动词/动词短语（`count_vowels`），不是 `f1`。
- [ ] 函数只做一件事，输入靠参数，结果靠 `return`。
- [ ] 我知道 `return` 和 `print` 的区别。
- [ ] 我知道函数里修改全局变量要 `global`，但更推荐用返回值。
- [ ] 我能读懂 `key=lambda s: (-s["score"], s["age"])`。
