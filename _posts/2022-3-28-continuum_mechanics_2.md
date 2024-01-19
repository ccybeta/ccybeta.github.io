---
title: 连续介质力学(二)：变形几何与运动学
author: cbtxs
date: 2022-03-28 15:02:30 +0800
mathjax: true
categories: [连续介质力学]
tags: [连续介质力学, 微分几何, 张量分析]
---

## **写在前面**
连续介质力学将物理上材料的变形问题转变为两个区域间的映射问题, 
变形前后的张量被拉回推前, 使得复杂的物理问题可以用数学的方法解决.

## **参考构型与当前构型**
一个材料在空间中占据的区域记为 $$\Omega$$, 经过一段时间 $$t$$ 后变成另一块区域
$$\Omega'$$, 记 $$\Omega$$ 为参考构型, $$\Omega'$$ 为当前构型. 那么存在一个映射
$$\boldsymbol\phi$$, 将 $$\Omega$$ 中的点 $$p$$ 映射为 $$p$$ 经过时间 $$t$$ 
后的位置 $$\boldsymbol\phi(p)$$, 使用笛卡尔坐标系表示(Lagrange视角)即为:

$$
\boldsymbol x = \boldsymbol\phi(\boldsymbol X, t)
$$

其中 $$\boldsymbol X$$ 是 $$p$$ 的坐标, $$\boldsymbol x$$ 是 
$$\boldsymbol\phi(p)$$ 的坐标. 引入变形梯度张量:

$$
\boldsymbol F = \frac{\partial x_i}{\partial X_j} 
\boldsymbol e_i \otimes \boldsymbol e_j = F_{ij}\ 
\boldsymbol e_i \otimes \boldsymbol e_j
$$

则有:

$$
\mathrm{d} \boldsymbol x = \boldsymbol F \mathrm d \boldsymbol X
$$

令 $$J = \mathrm{det}(F_{ij})$$, 表于当前构型与参考构型的体积比,
因为体积不会边的无穷大也不会变成 0, 所以 $$0 < J < \infty$$, 同时 $$J \neq 0$$
也是解存在唯一的条件.

















































