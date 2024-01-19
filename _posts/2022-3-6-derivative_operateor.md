---
title: 导数算符
author: cbtxs
date: 2022-03-06 14:26:32 +0800
katex: true
categories: [微分几何]
tags: [微分几何]
---

## **写在前面**
最近学习连续介质力学, 对之前一直不懂的**导数算符**有了一点新的理解,
故记录下来以备复习, 希望看这篇文章的同学也能学到一点东西.

新的理解简单来说就是:
<div align="center">

<b>与度规相配的导数算符, 就是这个度规下, 标准正交基组成的坐标系的普通导数算符.</b>
</div>

## **导数算符**
流形 $$M$$ 上的导数算符是一个 $$\mathscr T_{M}(l, m)$$ 到 
$$\mathscr T_{M}(l, m+1)$$ 的映射, 满足以下 5 个性质:

1. 具有线性性质;
2. 满足莱布尼茨律;
3. 与缩并可互换位置;
4. $$v(f) = v^a \nabla_a f$$;
5. 无挠性 : $$\nabla_a \nabla_b f = \nabla_b\nabla_a f$$.

可能大家看到这里有点蒙, 我对这里的定义的理解是, **流形上的导数算符可以认为是 
欧氏空间** $$(\mathbb R^3, \delta_{ab})$$ **中求导符号的推广**. 
首先普通流形与 $$(\mathbb R^3, \delta_{ab})$$ 相比, 1. 没有定义度量; 2.
没有定义坐标(坐标卡). 上面的 5 个条件就是在没有度量没有坐标系的情况下,
我们常见的求导符号所剩下的特征.

由定义可知, 不同导数算符作用在标量上是相同的, 但是作用在 
$$\mathscr T_{M}(l, m)$$ 上就不同了其中 $$(l>0\ or \ m>0)$$. 但是有如下定理:

**Theorem.**
$$\nabla_a$$ 和 $$\tilde\nabla_b$$ 是 $$M$$ 上的两个导数算符, $$w_b, w_b'$$ 
是两个对偶矢量场, 若 $$w_b|_p = w_b'|_p$$ 则有:

$$
[(\nabla_a - \tilde\nabla_a) w_b]_{p} = [(\nabla_a - \tilde\nabla_a) w_b']_p
$$

**Proof.** 略.                                        #

显然, $$(\nabla_a - \tilde\nabla_a)$$ 是将 $$p$$ 点处的一个对偶矢量映射成 $$p$$
点处的一个 (0, 2) 型张量. 所以 $$(\nabla_a - \tilde\nabla_a)$$ 对应于一个 (1, 2)
型张量 $$C_{ab}^c$$, 满足:

$$
[(\nabla_a - \tilde\nabla_a) w_b]_p = C^c_{ab} w_b|_p
$$

事实上有如下定理, 

**Theorem.**

$$
\nabla_a T^{c_0 c_1 ... c_l}_{b_0 b_1 ... b_m}
 = \tilde\nabla_a T^{c_0 c_1 ... c_l}_{b_0 b_1 ... b_m}
+ \sum_{i} C_{ad}^{c_i} T^{c_0 c_1 ... d ... c_l}_{b_0 b_1 ... b_m}
- \sum_{j} C_{ab_j}^{d} T^{c_0 c_1 ... c_l}_{b_0 b_1 ... d ... b_m}
$$

$$
\forall T \in \mathscr T_{M}(l, m)
$$

**Proof.** 略.                                     #

所以可以认为任意两个导数算符之间差一个 $$C_{bc}^a$$. ($$C_{bc}^a$$
有下标对称的性质, 这里就不展开表述了).

### **普通导数算符**
设 $${x^{\mu}}$$ 是 $$M$$ 上的坐标系, 坐标基矢场和为对偶坐标基矢场分别为 
$$\{(\partial x^{\mu})^a\}$$ 和 $$\{(\mathrm dx^{\mu})_a\}$$, $$O$$ 是坐标域, 
则可以定义映射 $$\partial_a$$:

$$
\partial_a : \mathscr T_{O}(k, l) \to \mathscr{T}_{O}(k, l+1)\\
$$

$$
\partial_a T_{c}^b := \partial_{\mu}T^{\nu}_{\sigma} 
(\mathrm dx^{\mu})_a (\partial x^{\nu})^b (\mathrm dx^{\sigma})_c
$$ 

其中 $$\partial_{\mu}T^{\nu}_{\sigma}$$ 表示 $$T^{\nu}_{\sigma}$$ 的偏导.
可以验证, 这个映射是一个导数算符, 称为坐标系 $$\{x^{\mu}\}$$ 的普通导数算符.

### **克氏符**
**Definition**
设 $$\partial_a$$ 是某一个坐标系的普通导数算符, 将导数算符 $$\nabla_a$$ 与
$$\partial_a$$ 之差记为 $$\Gamma_{ab}^c$$, $$\Gamma_{ab}^c$$ 称为 $$\nabla_a$$
在该坐标下的克氏符.

现在讨论这样一件事: **若 $$\{x^{\mu}\}$$ 和 $$\{x^{\mu}_0\}$$ 是 
$$M$$ 上的两个坐标系, 
则两个坐标系的普通导数算符 $$\partial_a, \partial_a^0$$ 之差是什么?**

记 $$\{(\partial x^{\mu})^a\}$$ 和 $$\{(\partial x^{\mu}_0)^a\}$$,
分别是两个坐标的坐标基矢, 则存在一个矩阵 $$A$$(定义在 $$M$$上), 使得: 

$$
(\partial x^{\mu})^a = A_{\mu\nu} (\partial x^{\nu}_0)^a
$$ 

则:

$$
(\mathrm dx^{\mu})_a = A^{\mu\nu}(\mathrm dx^{\nu}_0)_a, \quad
\frac{\partial f}{\partial x^{\mu}} = A_{\mu\nu} 
\frac{\partial f}{\partial x^{\nu}_0}
$$

若对偶向量 
$$w_a = w_{\mu}(\mathrm dx^{\mu})_a = w_{\nu}^0(\mathrm dx^{\nu}_0)_a$$, 
则:

$$
w_{\mu} = A^{\mu\nu} w^0_{\nu}
$$

所以

$$
\begin{aligned}
\partial_a w_b & = \partial_{\mu}w_{\nu} (\mathrm dx^{\nu})_b(\mathrm dx^{\mu})_a\\ 
\partial_a^0 w_b 
& = \partial_{\mu}^0w_{\nu}(\mathrm dx^{\nu}_0)_b(\mathrm dx^{\mu}_0)_a\\ 
& = \frac{\partial w_{\nu'}}{\partial x^{\mu'}_0} 
    A_{\nu\nu'}(\mathrm dx^{\nu})_b A_{\mu\mu'}(\mathrm dx^{\mu})_a\\ 
& = A^{\mu\mu'}\frac{\partial w_{\nu'}}{\partial x^{\mu}} 
    A_{\nu\nu'}(\mathrm dx^{\nu})_b A_{\mu\mu'}(\mathrm dx^{\mu})_a\\ 
& = A_{\nu\nu'}\partial_{\mu} (A^{\nu\nu'} w_{\nu})
    (\mathrm dx^{\nu})_b (\mathrm dx^{\mu})_a\\ 
& = A_{\nu\nu'}\partial_{\mu} (A^{\nu\nu'}) w_{\nu}
    (\mathrm dx^{\nu})_b (\mathrm dx^{\mu})_a
    + 
    \partial_{\mu}w_{\nu}
    (\mathrm dx^{\nu})_b (\mathrm dx^{\mu})_a
\end{aligned}
$$

记 $$\Gamma_{\mu\gamma}^{\nu} = A_{\nu\gamma}\partial_{\mu} (A^{\nu\gamma})$$,
是张量 $$\Gamma_{ab}^c$$ 的分量, 则:

$$
\Gamma_{ab}^{c} v_c 
= A_{\nu\gamma}\partial_{\mu} (A^{\nu\gamma}) v_{\nu}  
    (\mathrm dx^{\gamma})_b (\mathrm dx^{\mu})_a = (\partial_a^0 - \partial_a)
    v_b
$$




