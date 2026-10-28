# notes/ 学习笔记

每周一个文件：`week01.md` … `week18.md`。不要抄教程，只写自己的话。

建议模板：

```markdown
# 第 X 周笔记

## 这周学会的 3 件事
1.
2.
3.

## 代码片段（能复用的）
```python
# 只放 5–15 行，附一句说明
```

## 卡住的问题
- 现象：
- 原因：
- 解决：
- 下次怎么避免：

## 还没懂的
-
```

## 速查区（随学随加）

### 常用命令

```powershell
python --version
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
git status
git add .
git commit -m "week01: 完成初级和中级"
```

### 常用写法

```python
from pathlib import Path

p = Path("data") / "a.txt"
p.parent.mkdir(parents=True, exist_ok=True)
p.write_text("你好", encoding="utf-8")
text = p.read_text(encoding="utf-8")
```

> 自己的速查表比网上的大全有用：只记你实际用错过的。
