---
title: 变分原理
author: cbtxs
date: 2022-03-09 19:34:13 +0800
mathjax: true
categories: [泛函分析]
tags: [泛函, 变分, 微分几何]
---

## **写在前面**
变分是非常强力的数学工具, 在计算数学中非常常见,
冯康院士根据变分给出了有限元方法的数学原理, 开辟了有限元方法的研究,
是近代中国数学的巨大创新. 

变分最早可以追溯到牛顿解最速下降曲线时使用,
距今已经过去了好几百年, 我第一次见到 **变分** 这个词是在学有限元方法, 
那时候只知道变分就是对函数求导, 但是 **"对函数求导"** 是什么意思? 
这是我这两年半的研究生学习中最大的困惑, 这个神秘的 **变分方法**, 指引我学习基础的数学知识,
直到今天, 学到的所有知识交汇在一起, 终于, 我悟到了变分的本质:

<div align="center">
<b> 变分就是线性化 </b>
</div>

很简单的本质, 但是很多书上, 网上搜到的资料, 都没有讲这一点, 讲的都是关于 
Euler-Lagrange 方程, 对此我很不满意, 这并不应该是变分的全部,
这没有触及到变分的本质, 所以我就想讲一下我所理解的变分.

本文将会从泛函分析和微分几何两个角度理解变分, 
并将网上随处可以搜到的关于变分的知识结合,
尽可能的讲述 **变分**.

## **微分**
讲变分之前, 我先回顾一下数学分析中的微分. 

<div class="definition">
设函数 $f$ 为在 $x_0$ 周围有定义的函数, 若存在 $A \in \mathbb R$, 使得

$$
\Delta f = f(x_0+\Delta x) - f(x_0) = A \Delta x + O(\Delta x)
$$

则称 $f$ 在 $x_0$ 处可微, 微分为

$$
\mathrm df = A\mathrm dx
$$
</div>

特别的, 在梅加强版的数学分析中, 将 $$x \to Ax$$ 的线性映射称为 $$f$$ 在 $$x_0$$
处的微分.

对于 $$\mathbb R^n$$ 中的函数 $f$ 可以类似定义:
<div class="definition">
设函数 $f$ 为在 $\boldsymbol x_0 \in \mathbb R^n$ 周围有定义的函数, 
若存在 $A \in \mathbb R^n$, 使得

$$
\Delta f = f(\boldsymbol x_0+\Delta \boldsymbol x) - f(\boldsymbol x_0) 
= A \cdot \Delta \boldsymbol x + O(|\Delta \boldsymbol x|)
$$

则称 $f$ 在 $x_0$ 处可微, 微分为

$$
\mathrm df = A\cdot \mathrm d\boldsymbol x
$$
</div>
在梅加强版的数学分析中, 将 $$\boldsymbol x \to A\boldsymbol x$$ 的线性映射称为 
$$f$$ 在 $$\boldsymbol x_0$$ 处的微分.

## **变分**
关于泛函, 我们在网上常见的定义是下面这样:
<div class="definition">
令 $f \in C^1(\Omega\times\mathbb R\times\mathbb R^{n})$, 定义如下泛函:

$$
I(u) = \int_{\Omega} f(x, u(x), \nabla u(x)) \ \mathrm dx
$$
</div>

泛函的变分是这样的:
<div class="definition">
$\forall \phi \in C^1_0(\Omega)$, 可以定义 $I$ 关于 $\phi$ 的变分:

$$
\delta I(u_0, \phi) = \lim_{t \to 0} \frac{1}{t} (I(u_0+t\phi) - I(u_0))
$$
</div>

结束, 这就是我们最经常接触到的关于变分的知识, 这样的定义可能对于工科,
物理方面的学生很友好, 因为他们只需要会计算就行, 但是对于数学专业的学生来说,
这样的定义非常糟糕, 别的不说, 就只问一点: **泛函的变分是什么?** 在数学上,
他是个什么东西? 这个定义根本没有回答这个问题! 这也是我最开始学变分时最大的困惑.

要回答这一点, 我们还是要回到微分的定义, 从微分的定义出发看变分应该是个什么样子.
正如前面所说: 我们希望 $$f$$ 的微分存在, 需要存在一个 $$A \in R$$, 使得

$$
\Delta f(x_0) = f(x_0+\Delta x) - f(x_0) = A \Delta x + O(\Delta x)
$$

那类似的, 对于一个空间 $$V$$ 上的泛函 $$I$$ 我们可以直接这样写:

$$
\Delta I(u_0) = I(u_0 + \Delta u) - I(u_0) = A \Delta u + O(||\Delta u||_{V})
$$

那么问题来了,  $$A$$ 是什么? 是函数么? 很显然不是, 因为 $$I(u_0 + \Delta u) - I(u_0)$$ 
是实数! 那么 $$A\Delta u$$ 也是实数, 所以思来想去, **$$A$$ 只能是一个泛函!**,
而且与前面微分的对比, $$A$$ 还要是一个线性泛函, 定义在 $$V$$ 上. 
所以对于变分, 我们应该这样定义
<div class="definition">
设 $I$ 为空间 $V$ 上的一个泛函, 若能找到一个线性映射 $A \in V'$, 使得:

$$
\Delta I(u_0) = I(u_0 + \Delta u) - I(u_0) = A \Delta u + O(||\Delta u||_{V})
$$

对于任意的 $\Delta u \in V$ 成立, 则称 $A$ 是 $I$ 的变分.
</div>

既然说到这里了, 那我们再更进一步, $$V$$ 上的泛函是 $$V$$ 到 $$\mathbb R$$
上的映射, 那对于 $$V$$ 到任意其他空间 $$U$$ 上的的映射时不时也能类似的定义?
当然可以!

<div class="definition">
设 $U, V$ 是两个 Banach 空间, 对于一个映射 $F : U \to V$ 若存在一个线性映射
$A: U \to V$ 满足: $$\forall \epsilon > 0, \exists \delta > 0$$ 使得
$$
||F(u) - F(u_0) - A(u - u_0)||_{V} \leq \epsilon ||u-u_0||_{U}
$$
对于任意的 $||u - u_0|| < \delta$ 成立, 则称 $A$ 是 $F$ 的 Frechet 微分.
</div>


## **迭代算法**
考虑问题:

$$
\mathcal L(u) = f
$$

记 $$\mathcal L$$ 的变分为 $$\mathcal L_u$$, 任选 $$u_0$$, 
令 $$\delta u = u - u_0$$, 则有

$$
\mathcal L(u) = \mathcal L(u_0+\delta u) = \mathcal L(u_0) + \mathcal L_u(\delta u) + 
O(||\delta u||) = f
$$

舍去高阶项后得到一个以 $$\delta u$$ 为为质量的线性问题:

$$
\mathcal L_u(\delta u) = f - \mathcal L(u_0)
$$

令 $$u_1 = u_0 + \delta u$$, 得到一个迭代格式.


## **微分几何的角度**
从微分几何的角度来看, 所有常见的函数空间 $$V$$ 都是线性空间,
线性空间中每个元素 $$x$$ 处的切空间 $$T_xV$$ 与 $$V$$ 同构. 而 $$V$$
上的一个泛函 $$F$$ 就是 $$V$$ 到 $$R$$ 的一个映射, 其切映射 $$DF_x$$ 是
$$T_xV$$ 到 $$T_{F(x)}R$$ 的线性映射, 而:

$$
T_xV = V, \quad T_{F(x)}R = R
$$

所以 $$DF_x$$ 是 $$V$$ 到 $$R$$ 的线性映射, 所以 $$DF_x \in V'$$, 
不同的 $$x \in V$$ 有不同的切映射, 所以 $$DF$$ 是一个 $$V$$ 上的对偶矢量丛.
而这个 $$DF$$ 就是 $$F$$ 的变分, 所以说泛函的变分是一个对偶矢量场,
在每个函数处是一个线性泛函.





