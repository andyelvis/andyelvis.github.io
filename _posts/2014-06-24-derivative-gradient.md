---
layout: post
title: 方向导数和梯度
categories:
- machine learning
tags:
- gradient
---

##方向导数

在微积分课程中，函数在某一点的导数代表了函数在该点的变化率。
微分和积分，它们的定义都是建立在极限的基础上。
对于单变量函数$f(x)$，它在$x_0$处导数是：函数的改变量与自变量的改变量比值的极限。

$$
f'(x_0)=\lim_{\Delta x \to 0}\frac{f(x_0 + \Delta x)-f(x_0)}{\Delta x}
$$

对于单变量函数，自变量只有一个，当$x$趋近于$x_0$时只能在直线上变动，移动的方向只有左右两方。

然而，对于多变量函数，自变量有多个，表示自变量的点在一个区域内变动，不仅可以移动距离，而且可以按任意的方向来移动同一段距离。
因此，函数的变化不仅与移动的距离有关，而且与移动的方向有关。函数的变化率是与方向有关的。
这也才有了方向导数的定义，即某一点在某一趋近方向上的到数值。
假设给定函数$u=u(M)$，取一点$M_0=(x_0,y_0,z_0)$，L是$M_0$出发的任一半直线，则u在$M_0$点L的方向导数定义为：

$$
(\frac{\partial u}{\partial L})_{M_0}=\lim_{M \to M_0}_{M \in L}\frac{u(M)-u(M_0)}{|MM_0|}
$$

---

##梯度

有了方向导数的定义，进一步来推导方向导数的表示。假设L的方向余弦为$(\cos\alpha,\cos\beta,\cos\gamma)$，则L上的M可以表示为：

$$
x=x_0+t\cos\alpha, y=y_0+t\cos\beta,z=z_0+t\cos\gamma
$$

$$
t=|MM_0|
$$

于是u对L的方向导数为：

$$
\begin{align*}
(\frac{\partial u}{\partial L})_{M_0}=&\lim_{t \to 0}\frac{\Delta u}{t}\\
=&\lim_{t \to 0}\frac{\frac{\partial u}{\partial x} \Delta x + \frac{\partial u}{\partial y} \Delta y + \frac{\partial u}{\partial z} \Delta z + o(t)}{t}\\
=&\lim_{t \to 0}\frac{t(\frac{\partial u}{\partial x} \cos\alpha + \frac{\partial u}{\partial y} \cos\beta + \frac{\partial u}{\partial z} \cos\gamma) + o(t)}{t}\\
=&\frac{\partial u}{\partial x} \cos\alpha + \frac{\partial u}{\partial y} \cos\beta + \frac{\partial u}{\partial z} \cos\gamma
\end{align*}
$$

设向量$\overrightarrow{n}=(\frac{\partial u}{\partial x},\frac{\partial u}{\partial y},\frac{\partial u}{\partial z})$，
L方向可以表示为$\overrightarrow{l}=(\cos\alpha,\cos\beta,\cos\gamma)$。因为l是一个单位向量，所以：

$$
(\frac{\partial u}{\partial L})_{M_0}=n \cdot l=|n|\cos \theta
$$

这表示了L上的方向向量其实是n在L方向上的投影。当L的方向变化，投影量随之改变，也就代表了不同的方向导数。
当L与n同向时，$(\frac{\partial u}{\partial L})_{M_0}$便取得最大值|n|，我们称n为u在该点的梯度。
可以看到梯度即是某一点最大的方向导数，沿梯度方向函数有最大的变化率（正向增加，逆向减少）。