# 第 18 周作业：打包与发布（里程碑 M4）

> 📖 文档：[PyInstaller](https://pyinstaller.org/en/stable/) · [GitHub Release](https://docs.github.com/zh/repositories/releasing-projects-on-github)
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 把项目打包成 exe，在别的电脑/新目录能用；发布 v1.0.0。

## 本周安排

| 天 | 学习（约 30 分钟） | 作业（约 2.5 小时） |
| --- | --- | --- |
| 1 | PyInstaller 原理、`--onefile` | 初级 1–2 |
| 2 | 控制台/窗口模式、图标 | 初级 3 |
| 3 | 打包后的路径问题 | 中级 1–2 |
| 4 | 干净环境测试 | 中级 3 |
| 5 | README/CHANGELOG/Release | 高级 |
| 6 | 复盘、演示 | 复盘 |

## 作业

### 初级（必做，约 50 分钟）

1. 在项目 venv 里：
   ```powershell
   pip install pyinstaller
   pyinstaller --onedir --console main.py
   ```
   运行 `dist/main/main.exe`，确认能启动、能记账。
2. 改成单文件：
   ```powershell
   pyinstaller --onefile --console main.py
   ```
   对比 `--onedir` 和 `--onefile` 的启动速度、目录大小、杀毒误报情况，写进笔记。
3. 加窗口模式和图标：
   ```powershell
   pyinstaller --onefile --windowed --name 小账本 --icon assets/icon.ico main.py
   ```
   确认没有黑色控制台窗口；图标显示正常。

**验收**：两种模式都能运行；知道 `--windowed` 后看不到报错，调试时要换回 `--console`。

### 中级（必做，约 80 分钟）

1. **路径问题**：确认打包后数据库不在临时解压目录，而在固定位置：
   - 开发时：项目 `data/expense.db`；
   - 打包后：`%APPDATA%\ExpenseLite\expense.db`；
   - 用 `sys.frozen` 或 `getattr(sys, "frozen", False)` 判断，目录不存在自动建。
2. 处理资源文件：如果用了图标/图片，用 `sys._MEIPASS` 或 `Path(__file__).parent` 拼路径；在 `--onefile` 下测试。
3. **干净环境测试**：
   - 新建 `E:\test_expense\`（路径带空格也试一次）；
   - 只复制 exe 过去，双击运行；
   - 新增 2 条记录，关闭再开，数据还在；
   - 把 `%APPDATA%\ExpenseLite` 改名模拟首次运行，确认能自动重建。
4. 如果 Windows Defender 误报，记录你的处理方式（加信任/换 onedir），不要关闭杀毒软件。

**验收**：exe 在全新目录双击可用；数据写到 `%APPDATA%`；中文路径/空格路径不崩。

### 高级（挑战，约 50 分钟）

1. **文档定稿**：
   - `README.md`：功能介绍、截图、系统要求、安装（两种：源码运行 / 直接用 exe）、使用步骤、数据位置、备份与恢复、常见问题、版本；
   - `CHANGELOG.md`：`v1.0.0` 新增/修复/已知问题；
   - `requirements.txt`：开发依赖 + 打包依赖（可用注释分组）。
2. **发布**：
   - 确认 `.gitignore` 没有把源码/文档忽略；
   - 提交：`release: v1.0.0`；
   - 打标签：`git tag -a v1.0.0 -m "第一个可用版本"`，`git push origin v1.0.0`；
   - GitHub → Releases → 新建 `v1.0.0`，上传 exe（或压缩包），写更新说明。
3. **复盘**（`notes/week18.md`）：
   - 18 周实际用了多少小时？哪几周落后？
   - 最有用的 5 个知识点；
   - 最难的 3 个问题及解决方式；
   - 如果重来，会怎么调整路线；
   - 下一步学什么（从 ROADMAP 末尾挑 2 个）。
4. **3 分钟演示**：按“问题 → 功能 → 数据存哪 → 怎么打包 → 遇到什么坑”讲一遍，录音或写稿。

**验收**：GitHub Release 有 exe 和说明；tag 指向正确提交；别人下载 exe 能直接用；复盘不是流水账。

## 提交

- 代码/文档：`project/`
- 发布：Git tag `v1.0.0` + GitHub Release
- 笔记：`notes/week18.md`
- 进度：PROGRESS.md 第 18 行 + M4 + 毕业清单
- Git：`release: v1.0.0`

## 自检

- [ ] 我在“没有 Python 的电脑/新用户”场景下测试过（至少新目录 + 清环境变量）。
- [ ] 我知道 `--onefile` 每次启动会解压到临时目录，所以数据不能写在那。
- [ ] README 里的截图是最新界面。
- [ ] 版本号在窗口标题、关于、CHANGELOG、tag 四处一致。
- [ ] 我能不看书说出项目三层结构和数据表设计。
