# 李思雨毕业论文项目

本仓库用于管理硕士学位论文正文、答辩材料、图表结果、论文附件、归档文件和最终成果 PDF。主要内容已按中文目录归类，便于后续查看和提交。

## 目录结构

```text
.
├── main.tex                         # 兼容入口，编译时载入 论文正文/学位论文.tex
├── reference.bib                    # BibTeX 兼容入口，内容同步自 论文正文/参考文献.bib
├── 论文正文/
│   ├── 学位论文.tex                 # 学位论文主文件
│   ├── 摘要.tex                     # 中英文摘要
│   ├── 封面页.tex                   # 论文封面 LaTeX 页面
│   ├── 参考文献.bib                 # 中文命名的参考文献库管理副本
│   └── 图片资源/                    # 校徽、标题字体、不规则区域示意图等
├── 论文附件/                        # 封面、双盲审说明、独创性声明等 PDF 附件
├── 图表结果/                        # 论文和答辩共用图表、模拟结果、实证结果
├── 答辩材料/
│   ├── 答辩幻灯片.tex               # 答辩 slides 源文件
│   ├── 答辩逐字稿.tex               # 答辩讲稿源文件
│   └── 苏州大学校徽.jpeg
├── 论文情况介绍/
│   ├── 学位论文情况介绍.tex
│   └── 学位论文情况介绍.txt
├── 成果文件/                        # 需要随仓库保存和提交的成品 PDF
└── 归档/                            # 历史版本、旧 slides 和旧编译结果
```

## 成果文件

`成果文件/` 中保存当前需要提交或备份的结果文件：

```text
成果文件/学位论文正文.pdf
成果文件/学位论文情况介绍.pdf
成果文件/答辩幻灯片.pdf
成果文件/答辩逐字稿.pdf
```

这些 PDF 不在 `.gitignore` 中，应该随源码一起提交和 push。

## 编译论文

推荐仍从根目录编译 `main.tex`：

```powershell
latexmk -xelatex -interaction=nonstopmode -file-line-error -outdir=out main.tex
```

也可以直接编译中文主文件：

```powershell
latexmk -xelatex -interaction=nonstopmode -file-line-error -outdir=out 论文正文/学位论文.tex
```

编译输出目录 `out/` 是本地中间目录，默认不提交。确认结果无误后，可将最终 PDF 更新到 `成果文件/学位论文正文.pdf`。

说明：BibTeX 对中文路径支持不稳定，因此根目录保留一份 `reference.bib` 作为编译用入口；中文目录中的 `论文正文/参考文献.bib` 作为便于管理的副本保留。

## 编译答辩材料

答辩 slides：

```powershell
latexmk -xelatex -interaction=nonstopmode -file-line-error -outdir=答辩材料/out 答辩材料/答辩幻灯片.tex
```

答辩逐字稿：

```powershell
latexmk -xelatex -interaction=nonstopmode -file-line-error -outdir=答辩材料/out 答辩材料/答辩逐字稿.tex
```

确认结果后，可将输出 PDF 更新到 `成果文件/答辩幻灯片.pdf` 和 `成果文件/答辩逐字稿.pdf`。

## 图表维护

- 论文正文和答辩 slides 共用 `图表结果/` 中的图表。
- 更新模拟或实证图表时，优先替换 `图表结果/` 中的对应文件。
- `答辩材料/` 中不再保留重复图表副本，只保留答辩源码和标题页校徽。

## 归档说明

`归档/` 只保存历史版本和不再参与当前编译的文件：

- `归档/old_tex_versions/`：旧论文 tex 版本、旧摘要版本。
- `归档/defense_ppt_legacy/`：旧版答辩 slides、旧 bibliography、重复图表副本、原始压缩包。
- `归档/old_build_outputs/`：旧编译结果或历史检查输出。

归档文件不参与当前论文或答辩材料编译。需要恢复旧内容时，从对应归档目录复制回来即可。

## 版本管理建议

完成一轮明确修改后，可以执行：

```powershell
git status
git add .
git commit -m "整理毕业论文项目目录"
git push
```

编译中间文件、临时输出目录和本地 IDE 配置已写入 `.gitignore`，不应提交。
