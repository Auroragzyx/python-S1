# 资料与排错手册

## 主教材

- [菜鸟教程 Python 3 总目录](https://www.runoob.com/python3/python3-tutorial.html)
- [菜鸟教程 Git](https://www.runoob.com/git/git-tutorial.html)
- [菜鸟教程 SQLite](https://www.runoob.com/sqlite/sqlite-tutorial.html)
- [菜鸟教程 Tkinter](https://www.runoob.com/python/python-gui-tkinter.html)

## 常用章节直达（按 18 周顺序）

| 周 | 章节 |
| --- | --- |
| 1 | [基础语法](https://www.runoob.com/python3/python3-basic-syntax.html)、[基本数据类型](https://www.runoob.com/python3/python3-data-type.html)、[数据类型转换](https://www.runoob.com/python3/python3-type-conversion.html)、[注释](https://www.runoob.com/python3/python3-comment.html)、[运算符](https://www.runoob.com/python3/python3-basic-operators.html)、[数字](https://www.runoob.com/python3/python3-number.html) |
| 2 | [字符串](https://www.runoob.com/python3/python3-string.html) |
| 3 | [列表](https://www.runoob.com/python3/python3-list.html)、[元组](https://www.runoob.com/python3/python3-tuple.html)、[集合](https://www.runoob.com/python3/python3-set.html) |
| 4 | [字典](https://www.runoob.com/python3/python3-dictionary.html)、[条件控制](https://www.runoob.com/python3/python3-conditional-statements.html)、[循环](https://www.runoob.com/python3/python3-loop.html) |
| 5 | [函数](https://www.runoob.com/python3/python3-function.html)、[lambda](https://www.runoob.com/python3/python-lambda.html)、[推导式](https://www.runoob.com/python3/python-comprehension.html)、[迭代器与生成器](https://www.runoob.com/python3/python3-iterator-generator.html) |
| 6 | [模块](https://www.runoob.com/python3/python3-module.html)、[标准库](https://www.runoob.com/python3/python3-stdlib.html)、[日期和时间](https://www.runoob.com/python3/python3-date-time.html) |
| 7 | [输入输出](https://www.runoob.com/python3/python3-inputoutput.html)、[File](https://www.runoob.com/python3/python3-file-methods.html)、[OS](https://www.runoob.com/python3/python3-os-file-methods.html)、[with](https://www.runoob.com/python3/python3-with.html)、[错误和异常](https://www.runoob.com/python3/python3-errors-execptions.html)、[JSON](https://www.runoob.com/python3/python3-json.html) |
| 8 | [面向对象](https://www.runoob.com/python3/python3-class.html)、[命名空间/作用域](https://www.runoob.com/python3/python3-namespace-scope.html)、[类型注解](https://www.runoob.com/python3/python-type-hints.html) |
| 9 | [虚拟环境的创建](https://www.runoob.com/python3/python-venv.html)、[pip](https://www.runoob.com/python3/python3-pip.html) |

> 如果链接失效，回总目录按章节名找；教程是旧的，语法以 Python 官方文档为准。

## 官方文档（遇到教程没说清的回来查）

- [Python 中文文档](https://docs.python.org/zh-cn/3/)
- [内置函数](https://docs.python.org/zh-cn/3/library/functions.html)
- [字符串方法](https://docs.python.org/zh-cn/3/library/stdtypes.html#string-methods)
- [pathlib](https://docs.python.org/zh-cn/3/library/pathlib.html)
- [sqlite3](https://docs.python.org/zh-cn/3/library/sqlite3.html)
- [tkinter](https://docs.python.org/zh-cn/3/library/tkinter.html)
- [PyInstaller](https://pyinstaller.org/en/stable/)
- [pytest](https://docs.pytest.org/en/stable/)
- [Git 官方书（中文）](https://git-scm.com/book/zh/v2)

## 工具

| 工具 | 用途 | 备注 |
| --- | --- | --- |
| VS Code + Python 扩展 | 写代码、调试 | 装完按 `F5` 能调试 |
| Windows Terminal / PowerShell | 运行、venv、Git | 本路线默认 PowerShell |
| DB Browser for SQLite | 看表、跑 SQL | 第 11 周装，比命令行直观 |
| GitHub | 远程仓库、Release | 第 9 周开始用 |

## 报错排查四步

1. **读最后一行**：`SyntaxError` / `NameError` / `TypeError` / `KeyError` / `FileNotFoundError` 分别是什么意思。
2. **看行号**：从报错行往上找，通常是上一行少了括号/引号，或变量名拼错。
3. **打印中间值**：在关键位置 `print(type(x), repr(x))`，确认数据是不是你以为的那样。
4. **搜索原文**：复制报错最后一行（去掉路径里的用户名）去搜；搜不到就拆成最小可运行例子。

卡住超过 20 分钟：记录下来，先做别的题，复盘日再解决。**不要在一行报错上耗一晚上。**

## 常见坑

- **中文乱码**：读写文件统一 `encoding="utf-8"`；给 Excel 的 CSV 用 `utf-8-sig`。
- **路径反斜杠**：用 `pathlib.Path` 或原始字符串 `r"E:\data\a.txt"`。
- **PowerShell 不能激活 venv**：执行 `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`，再 `.\.venv\Scripts\Activate.ps1`。
- **`python` 不是内部命令**：安装时勾选 “Add python.exe to PATH”，或重装。
- **装了库却 import 失败**：确认 venv 已激活，`pip -V` 和 `python -V` 指向同一环境。
- **PyInstaller 打包后闪退**：先用 `--console` 打包看报错；数据库路径不要写死成相对路径。
- **杀毒误报**：PyInstaller 单文件 exe 常见，加信任或换 `--onedir`；不要为此关掉杀毒。
- **`tkinter` 找不到**：Windows 官方安装包默认带；微软商店版 Python 可能缺失，换官网安装包。

## 提问模板

```
环境：Windows 11 / Python 3.x / 是否 venv
目标：我想实现……
代码：（贴最小可运行代码，不要贴整个文件）
报错：（完整最后 10 行）
已试过：1. …… 2. ……
期望结果 vs 实际结果：
```

## 学习记录建议

每周笔记只写四行：**学了什么 / 做出什么 / 卡在哪 / 下周怎么办**。三个月后回头看，这比收藏一堆链接有用。
