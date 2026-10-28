# 第 10 周作业：工程化：结构、日志、测试

> 📖 复习：模块/包、异常；阅读 [pytest 入门](https://docs.pytest.org/en/stable/getting-started.html)
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 把脚本整理成包；会用 logging 记录；会用断点调试；会写 pytest 测试。

## 本周安排

| 天 | 学习（约 50 分钟） | 作业（约 2 小时） |
| --- | --- | --- |
| 1 | 包结构、入口、相对导入 | 初级 |
| 2 | logging 级别、格式、文件 | 中级 1 |
| 3 | 断点调试、读 traceback | 中级 2 |
| 4 | pytest 安装、断言、夹具概念 | 高级 1 |
| 5 | 测试异常与临时文件 | 高级 2 |
| 6 | 重做 + 写项目需求 | 复盘 |

## 作业

### 初级（必做，约 35 分钟）

把第 8 周的通讯录整理成可运行包：

```
code/week10/address_book/
├── __init__.py
├── __main__.py        # 入口：from .main import run; run()
├── models.py
├── storage.py         # 只管 JSON 读写
├── book.py            # ContactBook 业务逻辑
└── main.py            # 菜单/输入输出
```

要求：

- 在 `code/week10/` 下执行 `python -m address_book` 能启动；
- 从其它目录执行 `python -m` 不行也没关系，先理解“包要在父目录运行”；
- `storage.py` 不出现 `print`，`main.py` 不出现 `json`；
- 每个模块顶部写一句职责说明。

**验收**：`python -m address_book` 能跑；模块职责一眼能看懂；没有循环导入。

### 中级（必做，约 70 分钟）

1. **日志**：给项目加 `logging`：
   - 同时输出到控制台和 `logs/app.log`；
   - 格式：`时间 | 级别 | 模块 | 消息`；
   - 级别 `INFO`，文件用 `encoding="utf-8"`；
   - 记录：程序启动、添加联系人、删除联系人、保存失败；
   - 用 `RotatingFileHandler` 限制 1MB × 3 个文件（选做）。
2. **调试**：制造并修复 3 个 bug，每个都先用断点或 `print` 定位，再修：
   - 列表下标越界（删除最后一个后继续按原下标访问）；
   - `KeyError`（读取不存在的 JSON 字段）；
   - 除零（统计平均分时人数为 0）。
   
   把“现象 → 定位过程 → 根因 → 修法”写进 `notes/week10.md`。

**验收**：日志文件有中文且不乱码；三个 bug 都知道根因，不是靠试出来的。

### 高级（挑战，约 50 分钟）

1. 安装 pytest（在 venv 里），为 `storage.py` 和 `book.py` 写 **至少 6 个测试**，放在 `tests/`：
   - 保存后能读回；
   - 文件不存在时返回空列表；
   - JSON 损坏时抛指定异常或返回空并备份；
   - 添加重复姓名/手机号的处理；
   - 搜索大小写不敏感；
   - 删除不存在的联系人。
   
   用 `tmp_path` 夹具，不要往真实数据目录写测试数据。运行 `pytest -q` 全绿。
2. 写 `README.md`：项目一句话、环境要求、安装步骤、运行命令、测试命令。
3. 读 [PROJECT.md](../PROJECT.md)，用半页纸写你自己的“小账本”需求：3 条必须功能、2 条不做、1 张界面草图（手画拍照也行，文字描述也可）。第 13 周开始做。

**验收**：`pytest -q` 全绿且可重复运行；测试不依赖真实数据；README 能让别人跑起来。

## 提交

- 代码：`code/week10/address_book/`、`tests/`
- 文档：`README.md`、`docs/需求-小账本.md`
- 笔记：`notes/week10.md`（3 个 bug 的定位过程）
- 进度：PROGRESS.md 第 10 行
- Git：`week10: 完成工程化改造和测试`

## 自检

- [ ] 我知道 `python -m 包名` 和 `python 文件.py` 的运行差异。
- [ ] 我知道日志比 `print` 多了级别、时间、输出位置。
- [ ] 我会用 VS Code 在行号旁点红点、按 F5 单步调试。
- [ ] 我知道测试要覆盖正常、边界、异常三类情况。
- [ ] 我的测试不会因为运行顺序不同而失败。
