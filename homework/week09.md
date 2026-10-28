# 第 9 周作业：venv 与 Git

> 📖 教程：菜鸟教程“虚拟环境的创建” · [pip](https://www.runoob.com/python3/python3-pip.html) · [Git 教程](https://www.runoob.com/git/git-tutorial.html)
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 能独立建虚拟环境；会用 Git 记录、回滚、推送代码。

## 本周安排

| 天 | 学习（约 50 分钟） | 作业（约 2 小时） |
| --- | --- | --- |
| 1 | 为什么用 venv、创建/激活 | 初级 1–2 |
| 2 | pip、`requirements.txt`、镜像源 | 初级 3 |
| 3 | Git 四区、`init/add/commit/status/diff/log` | 中级 1–2 |
| 4 | `.gitignore`、分支、回滚 | 中级 3 |
| 5 | 远程仓库、push/pull | 高级 |
| 6 | 重做 + 笔记 | 复盘 |

## 作业

### 初级（必做，约 35 分钟）

1. 在本仓库根目录创建虚拟环境：
   ```powershell
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1
   python -V
   pip -V
   ```
   确认 `python` 和 `pip` 都指向 `.venv`。如果 PowerShell 报“禁止运行脚本”，执行：
   ```powershell
   Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
   ```
   然后把过程记进笔记。
2. 在 venv 里安装 `requests`，运行：
   ```python
   import requests
   print(requests.__version__)
   ```
   再执行 `pip freeze > requirements.txt`，打开文件看内容。
3. 退出 venv（`deactivate`），再运行 `python -c "import requests"`，观察是否还能导入，解释原因。

**验收**：能独立从零建环境；知道全局环境和 venv 的区别；`requirements.txt` 能复现安装。

### 中级（必做，约 70 分钟）

1. 在本仓库配置 Git 身份（只需一次）：
   ```powershell
   git config --global user.name "你的名字"
   git config --global user.email "你的邮箱"
   ```
   在 `code/week09/` 建一个小项目（可以是通讯录），执行 `git status` 看未跟踪文件。
2. 完成至少 **5 次有意义的提交**，每次只做一件事：
   - `week09: 初始化项目结构`
   - `week09: 添加联系人数据类`
   - `week09: 实现保存到 JSON`
   - `week09: 添加搜索功能`
   - `week09: 补充 README`
   
   每次提交前用 `git diff` 看一眼改了什么。
3. 补全 `.gitignore`（仓库已有，确认能忽略 `.venv/`、`__pycache__/`、`data/`、`dist/`），并用 `git status` 验证这些文件不再出现。
4. 故意改坏一个文件，用 `git restore 文件名` 撤销；再改一次，`git add` 后想撤销暂存，用 `git restore --staged 文件名`。把两条命令的区别写进笔记。

**验收**：`git log --oneline` 能看到 5 条清晰记录；工作区干净；能说清四区。

### 高级（挑战，约 50 分钟）

1. 把项目推到 GitHub：
   - 新建仓库（私有即可），不要勾选自动生成 README；
   - `git remote add origin <地址>`；
   - `git branch -M main`；
   - `git push -u origin main`。
2. 在网页上改一行 README，本地 `git pull` 同步；再本地提交一次并 `git push`。
3. 做一次“后悔药”实验：
   - 提交一次错误修改，用 `git revert` 撤销；
   - 或者本地未推送时用 `git reset --soft HEAD~1` 撤回提交但保留改动；
   - 把两条命令的适用场景写进 `docs/git-cheatsheet.md`。
4. 在 `docs/git-cheatsheet.md` 里整理至少 12 条常用命令，每条一句人话解释（不要抄整本教程）。

**验收**：GitHub 上能看到你的提交；能解释 `reset` / `revert` / `restore` 的区别；不会把 `.venv` 或数据库提交上去。

## 提交

- 代码：`code/week09/`
- 文档：`docs/git-cheatsheet.md`、`requirements.txt`
- 笔记：`notes/week09.md`（venv 激活过程、Git 四区、三条撤销命令的区别）
- 进度：PROGRESS.md 第 9 行
- Git：本周的提交本身就是作业，至少 5 次

## 自检

- [ ] 我知道 `.venv` 不能提交，但 `requirements.txt` 要提交。
- [ ] 我知道 `git add` 只是放进暂存区，`git commit` 才进本地仓库。
- [ ] 我知道提交信息要写“做了什么”，不是“update”。
- [ ] 我知道 `git pull` = `fetch` + `merge`。
- [ ] 我遇到冲突时不会直接删仓库重来。
