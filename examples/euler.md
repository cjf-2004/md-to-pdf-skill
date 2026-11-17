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
{\LARGE\heiti{欧拉公式的推导}}\\[0.5em]
{\normalsize 由泰勒级数到 $e^{i\theta}=\cos\theta+i\sin\theta$}
\end{center}
\vspace{0.3em}
```

# 一、要证明的等式

欧拉公式把指数函数与三角函数连在一起：对实数 $\theta$，

$$
e^{i\theta}=\cos\theta+i\sin\theta.
$$

取 $\theta=\pi$，就得到欧拉恒等式 $e^{i\pi}+1=0$。下面用泰勒级数推导。

# 二、三个泰勒展开

指数、余弦、正弦在 $0$ 处的展开对所有复数都成立：

$$
\begin{aligned}
e^{z}
&=\sum_{n=0}^{\infty}\frac{z^{n}}{n!}
=1+z+\frac{z^{2}}{2!}+\frac{z^{3}}{3!}+\frac{z^{4}}{4!}+\frac{z^{5}}{5!}+\cdots,\\[0.4em]
\cos z
&=\sum_{n=0}^{\infty}\frac{(-1)^{n}z^{2n}}{(2n)!}
=1-\frac{z^{2}}{2!}+\frac{z^{4}}{4!}-\cdots,\\[0.4em]
\sin z
&=\sum_{n=0}^{\infty}\frac{(-1)^{n}z^{2n+1}}{(2n+1)!}
=z-\frac{z^{3}}{3!}+\frac{z^{5}}{5!}-\cdots.
\end{aligned}
$$

# 三、代入 $z=i\theta$

令 $z=i\theta$，并反复用 $i^{2}=-1$、$i^{3}=-i$、$i^{4}=1$：

$$
\begin{aligned}
e^{i\theta}
&=1+i\theta+\frac{(i\theta)^{2}}{2!}+\frac{(i\theta)^{3}}{3!}+\frac{(i\theta)^{4}}{4!}+\frac{(i\theta)^{5}}{5!}+\cdots\\
&=1+i\theta-\frac{\theta^{2}}{2!}-i\frac{\theta^{3}}{3!}+\frac{\theta^{4}}{4!}+i\frac{\theta^{5}}{5!}+\cdots.
\end{aligned}
$$

把实部与虚部分开：实部恰好是 $\cos\theta$ 的级数，虚部系数恰好是 $\sin\theta$ 的级数，于是

$$
e^{i\theta}
=\Bigl(1-\frac{\theta^{2}}{2!}+\frac{\theta^{4}}{4!}-\cdots\Bigr)
+i\Bigl(\theta-\frac{\theta^{3}}{3!}+\frac{\theta^{5}}{5!}-\cdots\Bigr)
=\cos\theta+i\sin\theta.
$$

# 四、两个常用推论

令 $\theta=\pi$，因 $\cos\pi=-1$、$\sin\pi=0$，得到

$$
e^{i\pi}=\cos\pi+i\sin\pi=-1,
\qquad
e^{i\pi}+1=0.
$$

令 $\theta=\pi/2$，则 $e^{i\pi/2}=i$。一般地，单位圆上的点可写成 $e^{i\theta}$，复数乘法对应辐角相加：

$$
e^{i\alpha}e^{i\beta}=e^{i(\alpha+\beta)}.
$$
