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
{\LARGE\heiti{\xeCJKsetup{CJKecglue={}}第3版}}\\[0.5em]
{\normalsize 副标题（可删）}
\end{center}
\vspace{0.3em}
```

# 一、第一节

正文宋体，首行缩进两字。行内公式如 $e^{i\theta}=\cos\theta+i\sin\theta$。

独立公式：

$$
e^{z}=\sum_{n=0}^{\infty}\frac{z^{n}}{n!}.
$$

# 二、第二节

中文与英文专名之间留普通空格，例如 Taylor 级数与 Euler 公式。

## （1）小题

多行公式：

$$
\begin{aligned}
e^{i\theta}
&=1+i\theta-\frac{\theta^{2}}{2!}-i\frac{\theta^{3}}{3!}+\cdots,\\[0.4em]
\cos\theta+i\sin\theta
&=1-\frac{\theta^{2}}{2!}+\frac{\theta^{4}}{4!}+\cdots
+i\Bigl(\theta-\frac{\theta^{3}}{3!}+\cdots\Bigr).
\end{aligned}
$$

## （2）小题

矩阵：

$$
R(\theta)=\begin{pmatrix}\cos\theta&-\sin\theta\\ \sin\theta&\cos\theta\end{pmatrix}.
$$
