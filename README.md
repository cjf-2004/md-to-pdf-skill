# md-to-pdf

Claude Code 技能：用 **Markdown → Pandoc → XeLaTeX** 做出带真公式的中文 PDF。默认黑白、宋体/黑体、无页眉页脚。

这不是 [simonhaenisch/md-to-pdf](https://github.com/simonhaenisch/md-to-pdf)（那是 Puppeteer 打 HTML）。本仓库走 TeX，适合作业、笔记、带 `$...$` 的中文稿。

## 为什么走这条路

用 ReportLab 或浏览器打印硬画公式时，中易宋体没有数学字形，帽子、希腊字母、上下标会变成方框。Pandoc 把 Markdown 里的 `$` 交给 XeLaTeX，公式是真排版。

## 依赖

- [Pandoc](https://pandoc.org/installing.html)
- XeLaTeX：Windows 用 [MiKTeX](https://miktex.org/)，macOS 用 MacTeX，Linux 用 TeX Live（需 `ctex`、`xeCJK`、`amsmath`）
- 中文字体：Windows `SimSun` / `SimHei`；macOS `Songti SC` / `Heiti SC`；Linux `Noto Serif CJK SC` / `Noto Sans CJK SC`
- 检查用（可选）：Poppler 的 `pdfinfo`、`pdftoppm`

## 当作 Claude 技能安装

复制到个人技能目录，目录名保持 `md-to-pdf`：

```bash
git clone https://github.com/cjf-2004/md-to-pdf-skill.git md-to-pdf
```

常见位置：

- Claude Code：`~/.claude/skills/md-to-pdf`
- Claude Desktop（本机数据目录因平台而异）：`…/skills/md-to-pdf`

里面至少要有 `SKILL.md`。改完技能后新开一轮对话才会吃到更新。

## 自己编译一份

1. 复制 [`assets/template.md`](assets/template.md)，改标题和正文。
2. YAML **不要**写 `title:` / `author:`（否则 ctexart 会出页眉）。
3. 汉字紧贴数字的标题，用模板里那行 `\xeCJKsetup{CJKecglue={}}`，不要全局关掉 glue。
4. 编译：

```bash
pandoc doc.md -o doc.pdf --pdf-engine=xelatex -V CJKmainfont=SimSun -V CJKsansfont=SimHei
```

字体名按本机替换。逐步踩坑见 [`references/pitfalls.md`](references/pitfalls.md)。

## 仓库结构

```
SKILL.md                 Claude 技能正文（怎么写 MD、怎么编译、怎么检查）
assets/template.md       可直接复制的稿纸
references/pitfalls.md   YAML / xeCJK / 波浪号等坑
```

## License

MIT。见 [LICENSE](LICENSE)。
