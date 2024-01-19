---
title: 连续介质力学(一)：张量分析基础
author: cbtxs
date: 2022-03-04 22:19:01 +0800
mathjax: true
categories: [连续介质力学]
tags: [连续介质力学, 微分几何, 张量分析]
---

## **写在前面**
**连续介质力学** 是理性力学的基础.

连续介质力学中的数学部分是张量分析, 也是微分几何的基础, 
之前学过梁灿彬教授的 《微分几何与广义相对论》中的微分几何部分,
但是因为太过抽象, 理解的不够深刻, 这次学习的是
《连续介质力学》这本书, 书中重点讲的是 $$\mathbb R^3$$ 中的微分几何, 
像导数算符, 克氏符之前都是抽象的概念,
现在终于找到了具体的对应, 解决了很多我以前的疑惑,

本书的一的特点是, 基本上就把对偶向量当作了向量, 所以所有的 
$$(l, m)$$ 型张量都被当成了 $$(l+m, 0)$$ 型张量, 他们的基都是 

$$
\mathrm d\boldsymbol e_{i_0} \otimes
\mathrm d\boldsymbol e_{i_1} \otimes\dots\otimes
\mathrm d\boldsymbol e_{i_{l+m-1}} 
, \quad i_0, i_1, \dots, i_{l+m-1} \in \{0, 1, 2\}
$$

## **1. Kronecker 符号, Levi-Civita 符号**

设 $$\boldsymbol{\{e_0, e_1, e_2\}}$$ 为 $$\mathbb R^3$$ 中一组标准正交基, 则有:

$$
\boldsymbol{e_i \cdot e_j} = \delta_{ij}, \quad 
\boldsymbol{e_i \times e_j} = \in_{ijk} \boldsymbol{e_k}
$$

其中 $$\delta_{ij}$$ 是 Kronecker 符号, $$\in_{ijk}$$ 是 Levi-Civita 符号:

$$
\delta_{ij} = 
\begin{cases}
1 \quad i = j\\
0 \quad i \neq j 
\end{cases}
, \quad
\in_{ijk} = 
\begin{cases}
1 \quad \quad i, j, k \text{是偶排列}\\
-1 \ \quad i, j, k \text{是奇排列}\\
0 \quad \quad i, j, k \text{有重复指标}\\
\end{cases}
$$

Levi-Civita 符号满足下面恒等式:

$$
\in_{ijk}\in_{lmn} = \left| 
\begin{matrix}
\delta_{il} & \delta_{im} & \delta_{in}\\
\delta_{jl} & \delta_{jm} & \delta_{jn}\\
\delta_{kl} & \delta_{km} & \delta_{kn}\\
\end{matrix} \right|
$$

## 2. 赝标量, 赝矢量
首先引入两种坐标变换
1. **镜面反射**: 关于 $$\boldsymbol{e_y, e_z}$$ 所在平面的镜面反射:

  $$
  \boldsymbol{e}'_x = -\boldsymbol{e}_x,\quad
  \boldsymbol{e}'_y = \boldsymbol{e}_y,\quad
  \boldsymbol{e}'_z = \boldsymbol{e}_z.
  $$

2. **反演变换**: 

  $$
  \boldsymbol{e}'_x = -\boldsymbol{e}_x,\quad
  \boldsymbol{e}'_y = -\boldsymbol{e}_y,\quad
  \boldsymbol{e}'_z = -\boldsymbol{e}_z.
  $$

在空间反演下改变方向的是 **真矢量**, 否则是 **赝矢量**.
**两个真矢量的叉乘是赝矢量.**

**事实上在微分几何中, 令** $$V = \mathbb E^3$$, **真矢量对应于** $$\Lambda V$$ 
**中的元素, 赝矢量对应于 $$\Lambda^2 V$$ 中的元素.**

可以认为真矢量的基为 $$\boldsymbol e_0, \boldsymbol e_1, \boldsymbol
e_2$$, 真标量的基为 $$1$$, 而赝矢量的基为 
$$ \boldsymbol e_1 \times \boldsymbol e_2, \boldsymbol e_2 \times \boldsymbol e_0
, \boldsymbol e_0 \times \boldsymbol e_1$$, 赝标量的基为 $$ \boldsymbol e_0
\cdot (\boldsymbol e_1 \times \boldsymbol e_2)$$

令
$$
\boldsymbol u = u_i \boldsymbol e_i, 
\boldsymbol v = v_i \boldsymbol e_i
$$
则 

$$ 
\begin{aligned}
\boldsymbol u \times \boldsymbol v & = u_i \boldsymbol e_i \times v_j \boldsymbol e_j\\
& = (u_0 v_1 - v_0 u_1)\boldsymbol e_0 \times \boldsymbol e_1 + 
(u_1 v_2 - v_2 u_1)\boldsymbol e_1 \times \boldsymbol e_2 + 
(u_2 v_0 - v_0 u_2)\boldsymbol e_2 \times \boldsymbol e_0
\end{aligned}
$$

令 $$ \boldsymbol e_i' = -\boldsymbol e_i$$, 则: 
$$
\boldsymbol u = -u_i \boldsymbol e_i', 
\boldsymbol v = -v_i \boldsymbol e_i'
$$

$$ 
\begin{aligned}
\boldsymbol u \times \boldsymbol v & = (-u_i) \boldsymbol e_i' \times (-v_j) \boldsymbol e_j'\\
& = (u_0 v_1 - v_0 u_1)\boldsymbol e_0' \times \boldsymbol e_1' + 
(u_1 v_2 - v_2 u_1)\boldsymbol e_1' \times \boldsymbol e_2' + 
(u_2 v_0 - v_0 u_2)\boldsymbol e_2' \times \boldsymbol e_0'\\
& = (u_0 v_1 - v_0 u_1)\boldsymbol e_0 \times \boldsymbol e_1 + 
(u_1 v_2 - v_2 u_1)\boldsymbol e_1 \times \boldsymbol e_2 + 
(u_2 v_0 - v_0 u_2)\boldsymbol e_2 \times \boldsymbol e_0
\end{aligned}
$$

## 3. 逆变矢量, 协变矢量

对于一个线性空间 $$V$$, 其上的所有线性泛函组成其 **对偶空间(共轭空间)** $$V^*$$. 
逆变矢量就是 $$V$$ 中的元素, 协变矢量就是 $$V'$$ 中的元素. 

设 $$\boldsymbol{\{e_0, e_1, e_2\}}$$ 为 $$\mathbb R^3$$ 中一组基(**逆变基**), 取
$$\boldsymbol{e^0, e^1, e^2} \in (\mathbb R^3)'$$ 满足:

$$
\boldsymbol{e^i(e_j)} = \delta_{ij}
$$

则 $$\boldsymbol{e^0, e^1, e^2}$$ 是 $$(\mathbb R^3)'$$ 中的一组基(**协变基**). 当 $$V$$
上定义了度规以后, 根据 **里斯表示定理**, 存在 
$$\boldsymbol{e^{0*}, e^{1*}, e^{2*}} \in (\mathbb R^3)$$ 与 $$\boldsymbol{e^0, e^1, e^2}$$ 
对应.(逆变基在 $$V$$ 中的表示)

## 4.度规张量
前面讲的东西其实是有一些问题的:
为什么有标准正交基? 因为有向量内积? 那为什么有向量内积? $$\mathbb E^3$$
上天然有内积么? 不是的, 这是需要定义的, 即定义一个双线型泛函

$$
A : \mathbb E^3 \times \mathbb E^3 \to \mathbb R
$$

满足 3 个条件(内积的 3 个条件, 省略)

而度规张量就是内积的另一个名字. 内积的定义一般为:

$$
(u, v) = u \cdot v 
$$

而若 $$A$$ 是一个正定矩阵

$$
(u, v) = uAv = u_i A^{ij}v_i
$$

也是一个内积, 而其中 $$A^{ij}$$ 就是一个度规张量.

## 5. 克氏符
略

## 6. 哈密尔顿-凯莱定理
考虑一个 $$2$$ 阶张量 $$\boldsymbol S$$, 一个矢量 $$\boldsymbol v$$ 可以成为
$$\boldsymbol S$$ 的特征向量当:

$$
\boldsymbol {Sv} = \lambda \boldsymbol v 
$$

其中 $$\lambda$$ 是 $$\boldsymbol S$$ 的特征值. 
$$\lambda$$ 是 $$\boldsymbol S$$ 的特征值存在的充要条件是:

$$
\mathrm{det}(\boldsymbol{S} - \lambda \boldsymbol I) = 0
$$

记

$$
I_1 = \mathrm{tr}\boldsymbol S, \quad 
I_2 = \frac{1}{2}[(\mathrm{tr}\boldsymbol S)^2 - \mathrm{tr}S^2], \quad
I_3 = \mathrm{det} \boldsymbol S
$$

则:

$$
\mathrm{det}(\boldsymbol{S} - \lambda \boldsymbol I) = \lambda^3 - I_1\lambda^2
+ I_2\lambda -I_3
$$

<div class = "theorem">
<b>哈密尔顿-凯莱定理</b>: 任何一个 $(n\times n)$ 的矩阵都满足其特征方程.
</div>

## 7. 二阶张量的微积分
对于标量场 $$\phi$$, 定义其左右梯度如下:

$$
\nabla\otimes \phi = \frac{\partial \phi}{\partial x_i} \boldsymbol e_i, \quad
\phi \otimes \nabla = \frac{\partial \phi}{\partial x_i} \boldsymbol e_i.
$$

对于向量场 $$\boldsymbol v$$, 定义其左右梯度如下:

$$
\nabla\otimes \boldsymbol v = 
\frac{\partial v_j}{\partial x_i} \boldsymbol e_i \otimes \boldsymbol e_j, \quad
\nabla\otimes \boldsymbol v = 
\frac{\partial v_i}{\partial x_j} \boldsymbol e_i \otimes \boldsymbol e_j
$$

对于二阶张量场 $$\boldsymbol T$$, 定义其左右梯度如下:

$$
\nabla\otimes \boldsymbol T = 
\frac{\partial T_{jk}}{\partial x_i} \boldsymbol e_i \otimes \boldsymbol e_j
\otimes \boldsymbol e_k, \quad
\nabla\otimes \boldsymbol T = 
\frac{\partial T_{ij}}{\partial x_k} \boldsymbol e_i \otimes \boldsymbol e_j
\otimes \boldsymbol e_k
$$

















