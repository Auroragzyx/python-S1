# 第 7 周作业：文件、CSV/JSON、异常

> 📖 教程：[输入输出](https://www.runoob.com/python3/python3-inputoutput.html) · [File](https://www.runoob.com/python3/python3-file-methods.html) · [OS](https://www.runoob.com/python3/python3-os-file-methods.html) · [with](https://www.runoob.com/python3/python3-with.html) · [错误和异常](https://www.runoob.com/python3/python3-errors-execptions.html) · [JSON](https://www.runoob.com/python3/python3-json.html)
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 会用 `pathlib` 和 `with open` 读写文本；会存 CSV/JSON；出错时程序不崩。

## 本周安排

| 天 | 学习（约 50 分钟） | 作业（约 2 小时） |
| --- | --- | --- |
| 1 | 路径、`pathlib`、读文件 | 初级 1 |
| 2 | 写/追加、编码、`with` | 初级 2 |
| 3 | CSV 读写、JSON | 中级 1–2 |
| 4 | 异常处理、文件不存在 | 中级 3 |
| 5 | 挑战题 | 高级 |
| 6 | 重做 + 笔记 | 复盘 |

## 作业

### 初级（必做，约 35 分钟）

1. `file_basic.py`：
   - 用 `pathlib.Path` 在 `code/week07/data/` 下创建 `study.log`（目录不存在先 `mkdir(parents=True, exist_ok=True)`）；
   - 写入 3 行学习记录，再用追加模式写 2 行；
   - 读回全部内容并打印；
   - 统计行数、字符数；
   - 用 `for` 逐行读，去掉行尾换行后加行号输出。
2. 用 `Path.cwd()`、`Path(__file__)` 分别打印当前目录和本文件路径，把输出记到笔记，说清两者区别。
3. 故意读取一个不存在的文件，**先不捕获异常**，把报错最后一行抄进笔记，并指出错误类型名。

**验收**：中文写入/读出不乱码；知道 `"w"`、`"a"`、`"r"` 的区别；知道 `with` 会自动关闭文件。

### 中级（必做，约 70 分钟）

1. `contacts_csv.py`：把第 6 周的通讯录改成可保存：
   - 保存为 `data/contacts.csv`，表头 `name,phone,city`；
   - 启动时如果文件存在就读取，不存在就用空列表并提示“暂无数据”；
   - 添加/删除后自动保存；
   - 用 `newline=""` 和 `encoding="utf-8-sig"`，确保 Excel 打开中文正常。
2. `config.json`：用 JSON 保存 `{"theme": "light", "page_size": 20}`，实现 `load_config()` 和 `save_config()`：
   - 文件不存在时返回默认配置，不报错；
   - 修改 `page_size` 后写回，再读出来验证。
3. 给文件操作加上异常处理：捕获 `FileNotFoundError`、`PermissionError`、`UnicodeDecodeError`，分别给出中文提示，程序继续运行。

**验收**：删掉 CSV 再启动不崩；CSV 用 Excel 打开中文正常；JSON 文件内容可读。

### 高级（挑战，约 50 分钟）

`address_book_v1.py`：健壮版通讯录（可以基于第 6 周代码改）：

- 数据存 `data/contacts.json`，每次增删改后立即保存；
- 启动时自动加载；文件损坏（手动改坏 JSON）时提示“数据文件损坏”，并自动备份坏文件为 `contacts.json.bak`，然后用空数据启动；
- 输入校验：姓名不能为空、手机号必须是 11 位数字；
- 搜索不区分大小写；
- 关键操作写日志到 `data/app.log`：时间、操作、结果（用 `logging` 或简单追加文本都行，第 10 周会正式学 logging）；
- 写一个 `backup()`：把数据文件复制到 `data/backup/contacts_YYYYMMDD_HHMMSS.json`。

**验收**：手动破坏 JSON 后程序不崩且有提示；连续 5 次增删后重启，数据一致；日志能看到操作记录。

## 提交

- 代码：`code/week07/file_basic.py`、`contacts_csv.py`、`config.json` 相关代码、`address_book_v1.py`
- 数据：**不要提交** `data/` 里的真实数据，`.gitignore` 已忽略；可以提交一份 `samples/` 示例
- 笔记：`notes/week07.md`（三种编码/模式、异常类型、路径区别）
- 进度：PROGRESS.md 第 7 行
- Git：`week07: 完成初级和中级`

## 自检

- [ ] 我读写文件都写了 `encoding="utf-8"`。
- [ ] 我知道 `"w"` 会清空原文件，`"a"` 是追加。
- [ ] 我知道 `with open(...) as f:` 结束会自动关闭文件。
- [ ] 我捕获异常时写了具体类型，不是一把梭 `except:`。
- [ ] 我知道 CSV 是“逗号分隔的文本”，JSON 是“带结构的文本”，两者都不是 Excel 文件。
