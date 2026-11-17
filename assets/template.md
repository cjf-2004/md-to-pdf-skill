---
documentclass: ctexart
geometry: a4paper,margin=20mm
fontsize: 11pt
linestretch: 1.15
colorlinks: false
header-includes:
  - \pagestyle{empty}
  - \usepackage{amsmath,amssymb}
  - \setlength{\parindent}{2em}
  - \setlength{\parskip}{0.25em}
  - \setlength{\abovedisplayskip}{6pt}
  - \setlength{\belowdisplayskip}{6pt}
  - \setlength{\abovedisplayshortskip}{4pt}
  - \setlength{\belowdisplayshortskip}{4pt}
  - \ctexset{section/format={\large\heiti\raggedright},section/beforeskip=1.0ex plus .2ex,section/afterskip=0.5ex plus .1ex}
  - \ctexset{subsection/format={\zihao{-4}\heiti\raggedright},subsection/beforeskip=0.8ex plus .2ex,subsection/afterskip=0.4ex plus .1ex}
  - \raggedbottom
---

```{=latex}
\begin{center}
{\LARGE\heiti{\xeCJKsetup{CJKecglue={}}标题}}\\[0.5em]
{\normalsize 副标题（可删）}
\end{center}
\vspace{0.3em}
```

# 一、第一节

正文宋体，首行缩进两字。行内公式如 $\nabla F\cdot V=-F_t$。

独立公式：

$$
F(x,y,t)=F(x+\Delta x,\, y+\Delta y,\, t+\Delta t).
$$

# 二、第二节

中文与英文专名之间留普通空格，例如 Horn–Schunck 算法与 Lucas–Kanade 算法。

## （1）小题

多行公式：

$$
\begin{aligned}
u^{k+1}
&=\bar{u}^{k}
-\frac{F_x\bigl(F_x\bar{u}^{k}+F_y\bar{v}^{k}+F_t\bigr)}{\lambda^2+F_x^2+F_y^2},\\[0.4em]
v^{k+1}
&=\bar{v}^{k}
-\frac{F_y\bigl(F_x\bar{u}^{k}+F_y\bar{v}^{k}+F_t\bigr)}{\lambda^2+F_x^2+F_y^2}.
\end{aligned}
$$

## （2）小题

矩阵：

$$
v=(A^\top A)^{-1}A^\top b.
$$
