---
title: 高斯分布
date: 2018-01-04 22:17:39
categories: AI
tags:
	- PRML
	- probability
	- Gaussion-Distribution
---


# 1. Gaussion分布 #

## 1.1 基本性质 ##

(1) 求证：高斯分布满足归一化，即$\int_{-\infty}^{+\infty}{\mathcal N(x|\mu,\sigma^2)dx}=1$

证明：记
$$I=\int_{-\infty}^{+\infty}{\mathcal N(x|\mu,\sigma^2)dx}=\int_{-\infty}^{+\infty}{\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{1}{2\sigma^2}(x-\mu)^2}dx}$$
令$y=x-u$，则

$$
\begin{aligned}
I&=\int_{-\infty}^{+\infty}{\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{1}{2\sigma^2}y^2}dy} \\
I^2&=\int_{-\infty}^{+\infty}\int_{-\infty}^{+\infty}{\frac{1}{2\pi\sigma^2}e^{-\frac{1}{2\sigma^2}(u^2+v^2)}dudv}
\end{aligned}
$$

令$u=r\sin\theta, v=r\cos\theta$，则$dudv=rd\theta dr$，

$$
\begin{aligned}
I^2&=\int_{0}^{2\pi}\int_{0}^{+\infty}{\frac{1}{2\pi\sigma^2}e^{-\frac{1}{2\sigma^2}r^2}rdrd\theta}\\
&=\int_{0}^{2\pi}{\left[-\frac{1}{2\pi}e^{-\frac{1}{2\sigma^2}r^2}\right]_{r=0}^{+\infty}d\theta}\\
&=\int_{0}^{2\pi}{\frac{1}{2\pi}d\theta}=1
\end{aligned}
$$

$$
\begin{array}
{l}
\because \mathcal N(x|\mu,\sigma^2)\gt 0\\
\therefore I \gt 0,\; \int_{-\infty}^{+\infty}{\mathcal N(x|\mu,\sigma^2)dx}=1
\end{array}
$$

(2) 求证：高斯分布的期望（一阶矩）为均值$\mu$，即$\Bbb E[x]=\mu,\; x\sim\mathcal N(x|\mu,\sigma^2)$

证明：

$$\Bbb E[x]=\int_{-\infty}^{+\infty}{\mathcal N(x|\mu,\sigma^2)xdx}
=\int_{-\infty}^{+\infty}{\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{1}{2\sigma^2}(x-\mu)^2}xdx}$$

令$y=x-u$，则

$$
\begin{aligned}
\Bbb E[x]&=\int_{-\infty}^{+\infty}{\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{1}{2\sigma^2}y^2}(y+u)dy}\\
&=u\int_{-\infty}^{+\infty}{\mathcal N(y|1,\sigma^2)dy}+\int_{-\infty}^{+\infty}{\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{1}{2\sigma^2}y^2}ydy}\\
&=u+\left[\frac{-\sigma^2}{\sqrt{2\pi\sigma^2}}e^{-\frac{1}{2\sigma^2}y^2}\right]_{y=-\infty}^{+\infty}\\
&=u
\end{aligned}
$$

(3) 求证：高斯分布的二阶矩为$\mu^2+\sigma^2$，即$\Bbb E[x^2]=\mu^2+\sigma^2,\; x\sim\mathcal N(x|\mu,\sigma^2)$

证明： 已知高斯分布满足归一化，即$\int_{-\infty}^{+\infty}{\mathcal N(x|\mu,\sigma^2)dx}=1$，则

$$
\begin{aligned}
0&=\frac{\partial}{\partial\sigma^2}\int_{-\infty}^{+\infty}{\mathcal N(x|\mu,\sigma^2)dx}\\
&=\int_{-\infty}^{+\infty}{\left[\frac{\partial}{\partial\sigma^2}\mathcal N(x|\mu,\sigma^2)\right]dx}\\
&=\int_{-\infty}^{+\infty}{\left[
-\frac{1}{2\sigma^2}\mathcal N(x|\mu,\sigma^2) + \frac{(x-u)^2}{2\sigma^4}\mathcal N(x|\mu,\sigma^2)
\right]dx}\\
&=\int_{-\infty}^{+\infty}{\left[-\sigma^2\mathcal N(x|\mu,\sigma^2) + (x-u)^2\mathcal N(x|\mu,\sigma^2)\right]dx}\\
&=-\sigma^2 + \int_{-\infty}^{+\infty}{\mathcal N(x|\mu,\sigma^2)x^2dx} - \mu^2
\end{aligned}
$$

可得：

$$\Bbb E[x^2]=\int_{-\infty}^{+\infty}{\mathcal N(x|\mu,\sigma^2)x^2dx} = \mu^2+\sigma^2$$

# 1.2 多维高斯分布 #

$$\mathcal N({\bf x}|\mu, \Sigma)=\frac{1}{(2\pi)^{\frac D 2}\mid\Sigma\mid}\exp\left\{-\frac{1}{2}({\bf x}-\mu)^T{\mid\Sigma\mid}^{-1}({\bf x}-\mu)\right\}$$

# 1.3 高斯分布的最大似然估计 #

集合${\tt x}=(x_1,x_2,\ldots,x_N)^T$是对标量$x$的$N$次观测。假设这个集合的$N$个标量，独立的取自以$\mu$为均值，\sigma^2为方差的高斯分布，（独立取自同一分布的数据点，被称作独立同分布，independent and identically distributed, i.i.d）。

因为数据集${\tt x}$是独立同分布，则该数据集出现的概率为：

$$p({\tt x}|\mu,\sigma^2)=\prod_{n=1}^N\mathcal N(x_n|\mu,\sigma^2)\tag{1.3.1}\label{1.3.1}$$

公式$\eqref{1.3.1}$即是高斯分布的似然函数。根据观测数据集确定概率分布参数的一个通用标准是找到一组参数使得似然函数取得最大值（即该观测数据集出现的概率最大）。
<!-- 根据数据集在参数空间里搜索最符合观测结果的参数-->

公式$\eqref{1.3.1}$小概率连乘，容易造成计算精度下溢。通常取该似然函数的对数作为似然函数，由于对数函数单调递增，所以对数似然函数的最大值等价于原函数的最大值。

$$
\begin{aligned}
\arg\max_{\mu,\sigma^2}p({\tt x}|\mu,\sigma^2)&=\arg\max_{\mu,\sigma^2}\ln p({\tt x}|\mu,\sigma^2)\\
&=\arg\max_{\mu,\sigma^2}\sum_{n=1}^N\left\{-\frac{1}{2}\ln2\pi\sigma^2-\frac{1}{2\sigma^2}(x_n-\mu)^2\right\}\\
&=\arg\max_{\mu,\sigma^2}\left\{-\frac{1}{2\sigma^2}\sum_{n=1}^N{(x_n-\mu)^2}-\frac{N}{2}\ln\sigma^2-\frac{N}{2}\ln 2\pi\right\}
\end{aligned}
\tag{1.3.2}\label{1.3.2}
$$

$$
\arg\max_{\mu,\sigma^2}\ln p({\tt x}|\mu,\sigma^2)\Leftrightarrow
\begin{cases}
\frac{\partial}{\partial\mu}\ln p({\tt x}|\mu,\sigma^2)=0\\
\frac{\partial}{\partial\sigma^2}\ln p({\tt x}|\mu,\sigma^2) = 0
\end{cases}
\tag{1.3.3}\label{1.3.3}
$$

$$
\begin{aligned}
&\frac{\partial}{\partial\mu}\ln p({\tt x}|\mu,\sigma^2)=0\\
&\sum_{n=1}^N{-2(x_n-\mu_{ML})}=0\\
&\mu_{ML}=\frac{1}{N}\sum_{n=1}^N{x_n}
\end{aligned}
\tag{1.3.4}\label{1.3.4}
$$

$$
\begin{aligned}
&\frac{\partial}{\partial\sigma^2}\ln p({\tt x}|\mu,\sigma^2)=0\\
&\frac{1}{2\sigma^4}\sum_{n=1}^N\left\{(x_n-\mu)^2\right\}-\frac{N}{2\sigma^2}=0\\
&\sigma^2_{ML}=\frac{1}{N}\sum_{n=1}^N(x_n-\mu_{ML})^2
\end{aligned}
\tag{1.3.5}\label{1.3.5}
$$

