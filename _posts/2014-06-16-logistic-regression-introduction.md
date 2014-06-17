---
layout: post
title: 逻辑斯蒂回归模型
categories:
- machine learning
tags:
- logistic regression
---

## 1、逻辑斯蒂分布（logistic distribution）

设X是连续随机变量，X服从逻辑斯蒂分布是指X具有下列分布函数和密度函数：

$$
F(x)=P(X \le x)=\frac{1}{1+e^{-(x-\mu)/\gamma}}
$$

$$
f(x)=F^{'}(x)=\frac{e^{-(x-\mu)/\gamma}}{\gamma(1+e^{-(x-\mu)/\gamma})^2}
$$

$\mu$为位置参数，$\gamma>0$为形状参数。

逻辑斯蒂分布的密度函数f(x)和分布函数F(x)的图形如下图所示：
![](/images/logit_function.png)
分布函数属于逻辑斯蒂函数，其图形是一条S形曲线。改曲线以点$(\mu,\frac{1}{2})$为中心对称，即满足：

$$
F(-x + \mu)-\frac{1}{2}=-F(x - \mu)+\frac{1}{2}
$$

曲线在中心附近增长速度较快，在两端增长速度较慢。形状参数$\gamma$的值越小，曲线在中心附近增长得越快。

---

2、二项逻辑斯蒂回归模型

二项逻辑斯蒂回归模型是一种分类模型，由条件概率$P(Y|X)$表示，形式为参数化的逻辑斯蒂分布。
随机变量X取值为实数，随机变量Y取值为1或0。通过监督学习的方法来估计模型参数。

二项逻辑斯蒂回归模型是如下的条件概率分布：

$$
P(Y=1|x)=\frac{exp(w \cdot x+b)}{1+exp(w \cdot x+b)}
$$

$$
P(Y=0|x)=\frac{1}{1+exp(w \cdot x+b)}
$$

$x \in R^n$是输入，$Y \in \\{0,1\\}$是输出，$w \in R^n$和$b \in R$是参数，w称为权值向量，b称为偏置，$w \cdot x$为w和x的内积。

对于给定的输入实例x，按照公式求得$P(Y=1|x)$和$P(Y=0|x)$，
然后比较这两个条件概率的大小，将实例x分到概率值较大的那一类。 

为了方便，可以将权值向量和输入向量加以扩充，仍记作w，x，
即$w=(w^{(1)},w^{(2)},\cdot \cdot \cdot w^{(n)},b)^T$，$x=(x^{(1)},x^{(2)},\cdot \cdot \cdot x^{(n)},1)^T$。
这时，逻辑斯蒂回归模型如下：

$$
P(Y=1|x)=\frac{exp(w \cdot x)}{1+exp(w \cdot x)}
$$

$$
P(Y=0|x)=\frac{1}{1+exp(w \cdot x)}
$$

一个事件的几率是指该事件发生的概率与不发生概率的比值。如果事件发生的概率是p，那么该事件的几率是$\frac{p}{1-p}$，该事件的对数几率或logit函数是：

$$
logit(p)=log\frac{p}{1-p}
$$

对逻辑斯蒂回归而言，logit函数是：

$$
log\frac{P(Y=1|x)}{1-P(Y=1|x)}=w \cdot x
$$

这就是说，在逻辑斯蒂回归模型中，输入Y=1的对数几率是输入x的线性函数。或者说，输出Y=1的对数几率是由输入x的线性函数表示的模型，即逻辑斯蒂回归模型。

---

3、模型参数估计

逻辑斯蒂回归模型学习时，对于给定的训练数据集$T=\\{(x_1,y_1),(x_2,y_2),\cdot \cdot \cdot (x_N,y_N)\\}$，其中，$x_i \in R^n$，$y_i \in \\{0,1\\}$，可以应用极大似然估计法估计参数模型，从而得到逻辑斯蒂回归模型。

设：

$$
P(Y=1|x)=\pi(x)，P(Y=0|x)=1-\pi(x)
$$

似然函数为：

$$
\prod_{i=1}^{N}[\pi(x_i)]^{y_i}[1-\pi(x_i)]^{1-y_i}
$$

对数似然函数为：

$$
\begin{align*}
L(w)=&\sum^{N}_{i=1}[y_ilog\pi(x_i)+(1-y_i)log(1-\pi(x_i))]\\
=&\sum^{N}_{i=1}[y_ilog\frac{\pi(x_i)}{1-\pi(x_i)}+log(1-\pi(x_i))]\\
=&\sum^{N}_{i=1}[y_i(w \cdot x_i)-log(1+exp(w \cdot x_i))]
\end{align*}
$$

对L(w)求极大值，得到w的估计值。

问题变成了以对数似然函数为目标函数的最优化问题。逻辑斯蒂回归学习中通常采用的方法是梯度下降法和拟牛顿法。