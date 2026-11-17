# Markdown → PDF：踩过的坑和正确写法

改 YAML、标题、CJK 空格或公式前先看。这些是工具链问题，与文档主题无关。

## 1. 不要用 ReportLab 画公式

**错：** `Paragraph("grad F · V = - F_t")`、`u_bar^k`、`lambda`。中易宋体没有数学字形，帽子、希腊字母、上下标会变成方框或巨大空隙。

**对：** Markdown 写 `$...$` / `$$...$$`，Pandoc → XeLaTeX。

## 2. ctexart 默认页眉

**错：** YAML 写 `title: …`。ctexart 会在页眉印章节名（曾出现过页眉变成算法名），标题也变成带作者的正式题头。

**对：** 不要 `title:` / `author:`。用 `\pagestyle{empty}`，封面用 `{=latex}` 居中块。

## 3. 汉字+数字被拆开（「作业4」→「作业 4」）

xeCJK 在汉字和拉丁/数字之间插 `CJKecglue`。

试过但不够：

| 写法 | 结果 |
| --- | --- |
| Markdown 里直接写 `作业4` | 仍拆开 |
| `\mbox{作业4}` | 仍可能拆开 |
| 全局 `\xeCJKsetup{CJKecglue={}}` | 标题好了，正文「与 Lucas」粘成「与Lucas」 |
| `作业~4` 或 `与~Lucas` | 印出看得见的波浪号 |

**对：** 只在标题那几个字上关 glue，正文保持默认：

```latex
{\LARGE\heiti{\xeCJKsetup{CJKecglue={}}标题}}
```

写在 `{=latex}` 块里，不要放进 YAML。

## 4. YAML 把 `\xeCJKsetup{...}` 吃掉

**错：** 在 `header-includes` 里写未加引号的

```yaml
- \xeCJKsetup{CJKecglue={0.15em plus 0.05em minus 0.05em}}
```

`{` 被当成 YAML 映射，内容会漏进标题（曾变成 `作业0.15em plus 0.05em minus 0.05em4`）。

**对：** `header-includes` 不要写 `\xeCJKsetup`。glue 只写在 raw LaTeX 标题里。YAML 只保留模板里那些键。

## 5. Markdown `~` 会印出来

Pandoc 的 `~` 会进 PDF，不是「看不见的不断行空格」。

**对：** 普通空格 + 默认 xeCJK glue。专名用 en-dash `–`（U+2013），不要 `---`，也不要 `~`。

## 6. 空白尾页

**错：** 12 pt、默认 `displayskip`、默认 section skip → 多出几乎空白的最后一页。

**对：** 模板已是 11 pt、收紧的 display/section skip、`raggedbottom`。编译后看 `pdfinfo` 的 Pages。

## 7. 讲义 / 扫描 PDF 读法（输入侧）

- 有的读 PDF 工具会误报加密；`pdfinfo` 显示 `Encrypted: no` 时改用 `pdftotext` / `pdftoppm`
- 部分 Poppler 没有 `-jpeg`，用 `-png`
- 公式页必须看图，不要信纯文本抽取

## 8. 编译噪音

MiKTeX「have not checked for updates」、LaTeX 发行版年份和本机宏包年份不一致，都可以忽略。以 PDF 和 PNG 为准。

## 9. 正确编译

```powershell
# 若 pandoc / xelatex 不在 PATH，按本机安装位置追加
$env:Path = "$env:LOCALAPPDATA\Pandoc;$env:LOCALAPPDATA\Programs\MiKTeX\miktex\bin\x64;" + $env:Path
pandoc "doc.md" -o "doc.pdf" --pdf-engine=xelatex -V CJKmainfont=SimSun -V CJKsansfont=SimHei
if (-not $?) { exit 1 }
New-Item -ItemType Directory -Force -Path "preview" | Out-Null
pdftoppm -png -r 150 "doc.pdf" "preview/page"
pdfinfo "doc.pdf"
```

然后逐页看 PNG。macOS / Linux 把中文字体名换成系统里有的。
