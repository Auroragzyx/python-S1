# 第 14 周作业：Tkinter 基础

> 📖 教程：[Tkinter 教程](https://www.runoob.com/python/python-gui-tkinter.html) · [官方 tkinter 文档](https://docs.python.org/zh-cn/3/library/tkinter.html)
> 🕒 6 天 × 3 小时，第 7 天复盘
> 🎯 会开窗口、放控件、用 `pack`/`grid` 布局、绑定按钮事件、弹提示框。

## 本周安排

| 天 | 学习（约 50 分钟） | 作业（约 2 小时） |
| --- | --- | --- |
| 1 | 第一个窗口、`mainloop` | 初级 1 |
| 2 | `Label/Button/Entry`、事件 | 初级 2 |
| 3 | `pack` vs `grid`、`Frame` | 中级 1–2 |
| 4 | `messagebox`、输入校验 | 中级 3 |
| 5 | 小工具挑战 | 高级 |
| 6 | 重做 + 笔记 | 复盘 |

## 作业

### 初级（必做，约 35 分钟）

1. `hello_gui.py`：
   - 创建 480×320 窗口，标题“我的第一个界面”；
   - 窗口居中（用 `winfo_screenwidth/height` 算，别写死坐标）；
   - 放一个 `Label` 显示“你好，Python”；
   - 放一个 `Button`“点我”，点击后 Label 文字变成“你点了 1 次”，再点变 2 次；
   - 关闭窗口时正常退出。
2. 把窗口改成不可缩放（`resizable(False, False)`），观察效果，记到笔记。

**验收**：窗口能开能关；按钮点几次计数就对几次；没有控制台报错。

### 中级（必做，约 70 分钟）

`login.py`：登录表单。

- 用 `grid` 布局：标题、用户名、密码（`show="*"`）、登录、取消；
- 用户名/密码为空时，用 `messagebox.showwarning` 提示，不继续；
- 用户名 `admin`、密码 `123456` 时 `showinfo("登录成功")`，否则 `showerror("用户名或密码错误")`；
- 按回车等同点“登录”（`bind("<Return>", ...)`）；
- “取消”清空两个输入框并聚焦用户名；
- 用 `Frame` 把表单和按钮分两组，窗口拉伸时布局不乱。

**验收**：空输入有提示；回车能登录；密码显示为星号；布局不重叠。

### 高级（挑战，约 50 分钟）

`converter.py`：单位换算器（三选一，或做一个带多标签的）：

- 长度：米 ↔ 千米 ↔ 英里；
- 温度：摄氏 ↔ 华氏；
- 金额：元 ↔ 分（为项目做准备）。

要求：

- 输入框、下拉框（`ttk.Combobox`）选择换算类型、按钮“换算”、结果标签；
- 输入非数字时弹错误提示，不崩；
- 结果保留 2 位小数；
- 换算逻辑写成**独立函数**，界面只负责取值和显示（为第 16 周分层做准备）；
- 至少 3 组测试数据写进笔记。

**验收**：0°C = 32°F、100°C = 212°F；1 千米 = 1000 米；输入 `abc` 有提示。

## 提交

- 代码：`code/week14/hello_gui.py`、`login.py`、`converter.py`
- 笔记：`notes/week14.md`（`pack` vs `grid`、`StringVar` 预告、居中公式）
- 进度：PROGRESS.md 第 14 行
- Git：`week14: 完成 Tkinter 基础练习`

## 自检

- [ ] 我知道 `mainloop()` 会阻塞，后面的代码要放在它前面。
- [ ] 我知道同一个容器里不要混用 `pack` 和 `grid`。
- [ ] 我知道按钮的 `command` 传函数名，不带括号。
- [ ] 我知道 `Entry.get()` 拿到的是字符串。
- [ ] 我的窗口关闭后进程真的退出了。
