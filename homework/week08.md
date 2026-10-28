# 第 8 周作业：面向对象

> 📖 教程：[面向对象](https://www.runoob.com/python3/python3-class.html) · [命名空间/作用域](https://www.runoob.com/python3/python3-namespace-scope.html)
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 会定义类、创建对象；理解 `self`、实例属性、方法；会用类把数据和操作封装在一起。

## 本周安排

| 天 | 学习（约 50 分钟） | 作业（约 2 小时） |
| --- | --- | --- |
| 1 | 类、对象、`__init__`、`self` | 初级 |
| 2 | 实例方法、属性、`__str__` | 初级收尾 |
| 3 | 封装、私有属性、异常 | 中级 |
| 4 | 继承、`dataclass`、类型注解 | 中级收尾 |
| 5 | 挑战题 | 高级 |
| 6 | 重做 + 笔记 | 复盘 |

## 作业

### 初级（必做，约 35 分钟）

`book.py`：

1. 定义 `Book` 类：
   - 属性：`title`、`author`、`year`、`is_read`（默认 `False`）；
   - 方法 `summary()`：返回 `"《书名》 作者 (年份) - 已读/未读"`；
   - 方法 `mark_read()`：把 `is_read` 设为 `True`；
   - `__str__` 返回 `summary()` 的内容。
2. 创建 3 本书，其中一本标记已读，用 `print(book)` 输出。
3. 在笔记里画/写出：类、对象、属性、方法各是什么，`self` 指谁。

**验收**：不写 `Book.summary()` 这种调用错误；能解释 `__init__` 什么时候执行。

### 中级（必做，约 70 分钟）

`bank.py`：

1. 定义 `BankAccount`：
   - 属性：`owner`、`_balance`（初始 0）；
   - `deposit(amount)`：金额必须 > 0，否则 `raise ValueError("金额必须大于 0")`；
   - `withdraw(amount)`：金额 > 0 且不超过余额，否则抛 `ValueError`；
   - `balance` 属性（`@property`）只读返回余额；
   - `__str__` 输出 `"小明的账户余额：100.00 元"`。
2. 写 6 条测试（放在 `if __name__ == "__main__":`）：
   - 正常存 100、取 30；
   - 存 -10 报错；
   - 取 1000 报错；
   - 取 -5 报错；
   - 连续存取后余额正确。
   用 `try/except ValueError` 捕获并打印提示。
3. 用 `@dataclass` 定义 `Contact(name, phone, city)`，创建 2 个对象并打印，观察和普通类的区别。

**验收**：外部不能直接改 `_balance`（约定俗成）；错误输入不会让余额变化；能说出 `@property` 的用途。

### 高级（挑战，约 50 分钟）

把第 7 周的通讯录重构成 OOP 版 `address_book/`：

```
address_book/
├── main.py          # 只负责菜单和输入输出
├── models.py        # Contact 数据类
├── book.py          # ContactBook：增删改查、保存、加载、搜索
└── __init__.py
```

要求：

- `Contact` 用 `@dataclass`，字段 `name`、`phone`、`city`；
- `ContactBook` 内部用列表保存 `Contact` 对象，提供 `add/remove/search/list_all/save/load`；
- `save/load` 用 JSON，`Contact` 与 dict 互转；
- 手机号 11 位校验放在 `Contact` 或 `ContactBook` 里，不放在 UI 里；
- `main.py` 不直接碰 JSON，只调用 `ContactBook` 的方法；
- 在笔记里用文字画一张类图：`ContactBook` 有哪些属性、哪些方法，和 `Contact` 什么关系。

**验收**：从空数据开始添加 3 人、搜索、删除、退出、重启，数据还在；`main.py` 里没有 `json.load`。

## 提交

- 代码：`code/week08/book.py`、`bank.py`、`address_book/`
- 笔记：`notes/week08.md`（类/对象/self、`@property`、类图）
- 进度：PROGRESS.md 第 8 行
- Git：`week08: 完成初级和中级`

## 自检

- [ ] 我知道 `__init__` 不是构造函数，而是初始化方法。
- [ ] 我知道实例属性写在 `self.` 上，类属性写在类里。
- [ ] 我知道 `_name` 只是“别直接访问”的约定，不是真正私有。
- [ ] 我的类名用大驼峰（`ContactBook`），方法名用小写下划线。
- [ ] 我的类没有变成“什么都往里塞”的上帝类。
