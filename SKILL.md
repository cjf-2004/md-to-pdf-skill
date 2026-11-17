---
name: md-to-pdf
description: "把 Markdown 编成带真公式的中文 PDF：Pandoc + XeLaTeX，黑白朴素、无页眉页脚。用户要 md 转 pdf、Markdown→PDF、中文公式 PDF、Pandoc、XeLaTeX、公式排版难看要重排时都用本技能；不要用 ReportLab 直接画公式。"
---

# Markdown → PDF（Pandoc + XeLaTeX）

中文文档、尤其带数学公式时：先写 Markdown，再用 Pandoc 调 XeLaTeX。不要用 ReportLab / 浏览器打印冒充公式排版。

版式默认：**黑白、宋体/黑体、无页眉页脚、无彩色装饰。** 用户当次另有要求则覆盖默认。

## 依赖

编译前确认这些命令在 PATH 里（没有就先补上，再 `pandoc`）：

| 工具 | 作用 | 常见来源 |
| --- | --- | --- |
| `pandoc` | Markdown → XeLaTeX | [Pandoc](https://pandoc.org/installing.html) |
| `xelatex` | 出 PDF | Windows: MiKTeX；macOS/Linux: TeX Live / MacTeX |
| 中文字体 | xeCJK 主字体 / 黑体 | Windows：`SimSun`、`SimHei`；macOS：`Songti SC`、`Heiti SC`；Linux：`Noto Serif CJK SC`、`Noto Sans CJK SC` |
| `pdftoppm` | 把 PDF 栅格成 PNG 做目视检查 | Poppler |
| `pdfinfo` | 页数、纸张 | Poppler |

Windows 上 Pandoc / MiKTeX 经常不在默认 PATH，可按本机安装位置临时追加，例如：

```powershell
$env:Path = "$env:LOCALAPPDATA\Pandoc;$env:LOCALAPPDATA\Programs\MiKTeX\miktex\bin\x64;" + $env:Path
```

不要用 Windows Store 的占位 `python.exe` 去跑任何相关脚本。

字体名按上面表格换成当前系统有的；下面编译示例默认 Windows 的 `SimSun` / `SimHei`。

## 怎么写 Markdown

从 [assets/template.md](assets/template.md) 复制，改标题和正文。YAML 只保留模板里那些键。

### YAML

- `documentclass: ctexart`，`geometry: a4paper,margin=20mm`，`fontsize: 11pt`
- `colorlinks: false`
- `header-includes` 里必须有 `\pagestyle{empty}`（去掉 ctexart 默认页眉页脚）
- 装 `amsmath,amssymb`；收紧段距和公式上下空隙，避免末页大块空白
- 节标题左对齐黑体，不要居中花哨
- **不要**写 YAML `title:` / `author:`：ctexart 会做成带 running header 的正式题头

带花括号的 TeX **不要**直接丢进 YAML（见 [references/pitfalls.md](references/pitfalls.md)）。

### 标题

封面用 Pandoc raw LaTeX 块（围栏信息 `{=latex}`），不要用 Markdown `# 标题` 当封面。

汉字紧贴数字或拉丁字母时（「作业4」「第3版」），xeCJK 会插空变成「作业 4」。只在标题那几个字上关 glue，**不要**全局关掉（否则「与 Lucas」会粘成「与Lucas」）：

```latex
{\LARGE\heiti{\xeCJKsetup{CJKecglue={}}标题}}
```

完整块在模板里。

### 正文

- 一级节 `# 一、…`，小题 `## （1）…`（按文章结构改；不一定用中文编号）
- 行内 `$...$`，独立 `$$...$$`
- 多行 `aligned`，矩阵 `bmatrix`
- 中文与英文专名之间用**普通空格**
- 专名连接号用 en-dash `–`（U+2013）
- **不要**用 Markdown `~` 当不断行空格（会印出波浪号）

## 怎么编译

```powershell
pandoc "doc.md" -o "doc.pdf" --pdf-engine=xelatex -V CJKmainfont=SimSun -V CJKsansfont=SimHei
```

在源文件所在目录执行，或给 pandoc 绝对路径。输出用 ASCII 文件名更稳妥（中文名给部分附件通道会失败）。

macOS / Linux 把 `-V CJKmainfont=` / `-V CJKsansfont=` 换成系统里实际有的字体名。

## 检查

1. `pdfinfo doc.pdf`：页数、纸张 A4。不要无故多出空白尾页。
2. `pdftoppm -png -r 150 doc.pdf page`（部分 Poppler 没有 `-jpeg`，用 `-png`）
3. **看每一页 PNG**：无页眉页脚、标题是否被拆开、公式是否真排版、有无裸露的 `~` 或 YAML 残渣。

未看图不要说 PDF 已完成。

MiKTeX「have not checked for updates」、LaTeX release 年份警告可忽略，以 PDF 和 PNG 为准。

改 YAML、标题或 CJK 空格之前先读 [references/pitfalls.md](references/pitfalls.md)。
