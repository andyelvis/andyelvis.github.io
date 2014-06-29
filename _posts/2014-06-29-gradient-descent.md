---
layout: post
title: 梯度下降法
categories:
- machine learning
tags:
- gradient descent
---

梯度下降法是一种一阶优化算法。一个函数在当前点沿着负梯度方向移动，可以找到局部最小值。
相反，沿着正梯度方向移动，可以找到局部最大值，这个时候就叫梯度上升法了。

如果多变量函数$F(x)$在点$a$处有定义且可微，那么$F(x)$从$a$处沿着负梯度方向$\nabla F(a)$移动，下降最快。

设：

$$
b=a-\gamma \nabla F(a)
$$

对于$\gamma$足够小，那么$F(a) \ge F(b)$。

按照这个逻辑，对于$x_0,x_1,x_2,\cdot \cdot \cdot$，

$$
x_{n+1}=x_n- \gamma_n \nabla F(x_n),n \ge 0
$$

我们可以得到：

$$
F(x_0) \ge F(x_1) \ge F(x_2) \ge \cdot \cdot \cdot
$$

序列$(x_n)$收敛到期望的局部最小值，步长$\gamma$允许在每次迭代的时候发生变化。当函数F是凸函数的时候，所有的局部最小值也就是全局最小值。

如果给定函数在不同方向的变化速率不同，那么梯度下降法在规定精度下，需要迭代很多次才能计算出一个局部最小值。
对于有些函数，预处理，可以变换几何空间使得函数的水平集像同心圆，从而可以改善收敛慢的问题。然而，构造和应用预处理，计算代价也很大。

梯度下降法也可以和线性搜索结合起来使用，在每次迭代的时候找到最优的步长$\gamma$。
但是，执行线性搜索非常耗时，使用固定的$\gamma$又会导致很差的收敛性。

牛顿法和使用共轭梯度的海森矩阵转置法是更好的选择。这几种方法收敛需要的迭代次数要少一些，但是每次迭代的计算消耗也大一些。
例如BFGS方法，每一步需要计算一个梯度向量与一个矩阵的乘积来确定一个更好的方向，同时使用一个复杂的线性搜索算法找到最好的步长$\gamma$。

逻辑斯蒂回归模型的负梯度方向：

$$
\begin{align*}
\frac{\partial u}{\partial w}L(w)=&\frac{\partial u}{\partial w}(-\sum^{N}_{i=1}[y_i(w \cdot x_i)-log(1+exp(w \cdot x_i))])\\
=&\sum^{N}_{i=1}[\frac{1}{1+exp(w \cdot x_i)} \cdot exp(w \cdot x_i) \cdot x_i - y_i \cdot x_i]\\
=&\sum^{N}_{i=1}[\frac{exp(w \cdot x_i)}{1+exp(w \cdot x_i)} - y_i]x_i
\end{align*}
$$