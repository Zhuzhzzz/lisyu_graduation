# 版本管理说明

当前项目已经使用 Git 管理。以后可以这样操作：

```powershell
git status
git add .
git commit -m "说明这次改了什么"
```

查看历史版本：

```powershell
git log --oneline
```

临时查看某个旧版本的文件：

```powershell
git show 提交号:main.tex
```

回退到上一个提交中的某个文件：

```powershell
git restore main.tex
```

如果要把整个项目回到某个历史版本，先确认没有未保存修改，再执行：

```powershell
git restore --source 提交号 .
```

建议每完成一轮明确修改就提交一次，例如“调整封面”“修改第五章实证图”“修正参考文献格式”。
