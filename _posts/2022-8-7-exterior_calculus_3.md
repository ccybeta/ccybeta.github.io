---
title: 有限元外微分(三)：同调代数
author: cbtxs
date: 2022-08-07 17:04:14 +0800
katex: true
comments : true
categories: [偏微分方程数值解]
tags: [微分几何, 偏微分方程数值解, 有限元]
---

## 写在前面
本文讲有限元中涉及到的同调代数

## **de Rham 复形**
de Rham 复形是一列空间和映射:

$$
0 \to \Lambda^0(\Omega) \xrightarrow{ \mathrm{d}}
 \Lambda^1(\Omega) \xrightarrow{ \mathrm{d}} \cdots \xrightarrow{ \mathrm{d}}
 \Lambda^n(\Omega) \to 0
$$

因为 $$\mathrm{d}\circ \mathrm{d} = 0$$, 所以 $$\forall k \in \{0, 1, \cdots, n\}$$:

$$
\mathcal{R}( \mathrm{d}: \Lambda^{k-1}(\Omega) \to \Lambda^k(\Omega)) \subset
\mathcal{N}( \mathrm{d}: \Lambda^{k}(\Omega) \to \Lambda^{k+1}(\Omega))
$$

所以称这个函数空间和映射的序列为一个 **上链复形**. de Rham 上同调空间 
$$H_{dR}^k$$ 是零空间与像空间的商空间: 

$$
H_{dR}^k = \frac{\mathcal{N}
(\mathrm{d}: \Lambda^{k}(\Omega) \to \Lambda^{k+1}(\Omega))}
{\mathcal{R}
(\mathrm{d}: \Lambda^{k-1}(\Omega) \to \Lambda^{k}(\Omega))}
$$

即: 当 $$w_1, w_2 \in 
\mathcal{N}( \mathrm{d}: \Lambda^{k}(\Omega) \to \Lambda^{k+1}(\Omega))$$
且 $$w_1-w_2 \in 
\mathcal{R}( \mathrm{d}: \Lambda^{k-1}(\Omega) \to \Lambda^k(\Omega))
$$
则在 $$H_{dR}^k$$ 中 $$w_1 = w_2 = [w_1]$$. $$H_{dR}^k$$ 的维数等于 $$\Omega$$
的 **Betti 数**

上面讲的是光滑的 de Rham 复形, 那么类似地可以定义 $$L^2$$ de Rham 复形:

$$
0 \to H\Lambda^0(\Omega) \xrightarrow{ \mathrm{d}}
 H\Lambda^1(\Omega) \xrightarrow{ \mathrm{d}} \cdots \xrightarrow{ \mathrm{d}}
 H\Lambda^n(\Omega) \to 0
$$

那么 $$H_{dR}^{k}$$ 同构于调和函数空间 $$\mathfrak{H}^k$$:

$$
\mathfrak{H}^{k}(\Omega) = \{\omega \in H\Lambda^{k}(\Omega)| \mathrm{d}\omega =
0, \langle\omega, \mathrm{d}\eta\rangle_{L^2\Lambda^k} = 0\ \forall \eta \in
H\Lambda^{k-1}(\Omega)\}
$$

事实上, $$\mathfrak{H}^{k}(\Omega) = 
\mathcal{N}( \mathrm{d}: \Lambda^{k}(\Omega) \to \Lambda^{k+1}(\Omega)) \cap
\mathcal{R}^{\perp}( \mathrm{d}: \Lambda^{k-1}(\Omega) \to \Lambda^k(\Omega))$$
所以这个同构关系很显然.

当 $$\Omega$$ 是一个单连通区域, 所有的上同调空间都是 $$0$$. 此时称复形:

$$
0 \to \Lambda^0(\Omega) \xrightarrow{ \mathrm{d}}
 \Lambda^1(\Omega) \xrightarrow{ \mathrm{d}} \cdots \xrightarrow{ \mathrm{d}}
 \Lambda^n(\Omega) \to 0
$$

是恰当的

## **余微分算子**
定义余微分算子: $$\delta: \Lambda^k(\Omega) \to \Lambda^{k-1}(\Omega)$$:

$$
\star \delta \omega = (-1)^k \mathrm d \star \omega, \quad \omega \in
\Lambda^k(\Omega)
$$

则根据内积定义有:

$$
\langle \mathrm{d}\omega, \eta \rangle = \langle \omega, \delta \eta \rangle  + 
\int_{\partial\Omega} \mathrm{Tr} \omega \wedge \mathrm{Tr} \star \eta, \quad
\omega \in \Lambda^k(\Omega), \eta \in \Lambda^{k+1}(\Omega)
$$

当 $$\omega$$ 或 $$\eta$$ 的迹为 $$0$$ 时, 

$$
\langle \mathrm{d}\omega, \eta \rangle = \langle \omega, \delta \eta \rangle
$$

即, $$\delta$$ 是 $$\mathrm d$$ 的共轭算子. 类比与 $$H\Lambda^k$$, 可以定义:

$$
H^*\Lambda^k(\Omega) = \{\omega \in L^2\Lambda^k(\Omega)| \delta \omega \in
L^2\Lambda^{k-1}(\Omega)\}
$$

显然有: $$H^*\Lambda^k(\Omega) = \star H\Lambda^{n-k}(\Omega)$$, 且有对偶复形:

$$
0 \leftarrow H^*\Lambda^0(\Omega) \xleftarrow{ \delta} \cdots 
\xleftarrow{ \delta} H^*\Lambda^n(\Omega) \leftarrow 0
$$

## **边界迹**
迹算子 $$ \mathrm{Tr}: \Lambda^k(\Omega) \to \Lambda^k(\partial \Omega)$$
可以认为是 Sobolve 空间中 $$H^1\Lambda^k(\Omega)$$ 到 
$$H^{1/2}\Lambda^k(\partial\Omega)$$的迹算子的扩展. 对于 $$\omega \in
H\Lambda(\Omega)$$ 其迹的意义如下: 

对于 $$\rho \in H^{1/2}\Lambda^k(\partial
\Omega)$$, 用 $$\bar{\star} \rho$$ 表示 $$\rho$$ 关于边界 $$\partial \Omega$$
的 Hodge star, 则必定存在一个 $$\eta \in H^1\Lambda^{n-k-1}(\Omega)$$ 使得 
$$ \mathrm{Tr} \eta = \bar{\star}\eta$$, 且有:

$$
||\eta||_{H^1} \leq c||\bar{\star}\rho||_{H^{1/2}} \leq c ||\rho||_{H^{1/2}}
$$

则对于任意的 $$\omega \in \Lambda^k(\Omega)$$ 有:

$$
\begin{aligned}
\langle \mathrm{Tr}\omega, \rho \rangle & = \int_{\partial \Omega}
\mathrm{Tr}\omega \wedge \bar{\star}\rho\\
& = \int_{\partial\Omega}
\mathrm{Tr}\omega \wedge \mathrm{Tr} \eta\\
& = \int_{\Omega} [ \mathrm{d} \omega \wedge \eta + (-1)^k\omega \wedge \delta
\eta] \\
& \leq||\omega||_{H\Lambda}||\eta||_{H^1}\\
& \leq||\omega||_{H\Lambda}||\rho||_{H^{1/2}}
\end{aligned}
$$

定义:

$$
\mathring{H}\Lambda^k(\Omega) = \{\omega \in H\Lambda^k(\Omega)|
\mathrm{Tr}\omega = 0\} 
$$

若 $$\omega \in H^*\Lambda^k(\Omega)$$, 则 $$\star\omega \in 
H\Lambda^{n-k}(\Omega)$$, 所以 $$ \mathrm{Tr}$$ 有意义, 有:

$$
\mathring H^*\Lambda^k(\Omega) := \star \mathring H\Lambda^{n-k}(\Omega)
 = \{\omega \in H^*\Lambda^k(\Omega)| \mathrm{Tr} \star\omega = 0\}
$$

若 $$\omega$$ 光滑, 则 
- $$ \mathrm{Tr}\omega = 0$$ 当且仅当 $$\omega_x$$ 的切向分量为 $$0$$; 
- $$ \mathrm{Tr}\star\omega = 0$$ 当且仅当 $$\omega_x$$ 的法向分量为 $$0$$.

有以下结论:

$$
\{\omega \in L^2\Lambda^k(\Omega) | \langle \omega, \mathrm{d}\eta
\rangle_{L^2\Lambda^{k}(\Omega)} = 0, \ \forall \eta \in H\Lambda^{k-1}(\Omega) \}
= \{\omega \in \mathring H^*\Lambda^k(\Omega) | \delta \omega = 0\}
$$

$$
\{\omega \in L^2\Lambda^k(\Omega) | \langle \omega, \delta \eta
\rangle_{L^2\Lambda^{k}(\Omega)} = 0, \ \forall \eta \in H\Lambda^{k+1}(\Omega) \}
= \{\omega \in \mathring H\Lambda^k(\Omega) | \mathrm{d} \omega = 0\}
$$

且有:

$$
\mathfrak{H}^k = \{\omega \in H\Lambda^k(\Omega) \cap \mathring H^*\Lambda^k
(\Omega) | \mathrm{d} \omega = 0, \delta \omega =0\}
$$


<p style="color:red"><b>以上三个结论需要证明</b></p>


## **带有边界条件的上同调**
用 $$\mathring \Lambda^k(\Omega)$$ 表示 $$\Lambda^k(\Omega)$$
中带有紧支集的光滑 $$k-$$形式 组成的子空间. 因为推前算子和微分算子可交换, 所以
$$ \mathrm{Tr (d} \omega) = \mathrm{d (Tr}\omega)$$, 所以 
$$ \mathrm{d} \mathring \Lambda^k(\Omega) \subset \mathring \Lambda^{k+1}(\Omega)$$
有如下的 de Rham 复形:

$$
0 \to \mathring \Lambda^0(\Omega) \xrightarrow{ \mathrm{d}}
\mathring \Lambda^1(\Omega) \xrightarrow{ \mathrm{d}} \cdots
 \xrightarrow{ \mathrm{d}}\mathring \Lambda^n(\Omega) \to 0 
$$

因为在 $$ H\Lambda^k(\Omega)$$ 中 $$ \mathring \Lambda^k(\Omega)$$ 的闭包为
$$ \mathring H\Lambda^k(\Omega)$$, 所以有以下复形:

$$
0 \to \mathring H \Lambda^0(\Omega) \xrightarrow{ \mathrm{d}}
\mathring H \Lambda^1(\Omega) \xrightarrow{ \mathrm{d}} \cdots
 \xrightarrow{ \mathrm{d}}\mathring H \Lambda^n(\Omega) \to 0 
$$

复形的上同调空间为:

$$
\mathfrak{ \mathring H}^{k}(\Omega) = \{\omega \in \mathring H\Lambda^{k}(\Omega)| \mathrm{d}\omega =
0, \langle\omega, \mathrm{d}\eta\rangle_{L^2\Lambda^k} = 0\ \forall \eta \in
\mathring H\Lambda^{k-1}(\Omega)\}
$$

同理有:

$$
\{\omega \in L^2\Lambda^k(\Omega) | \langle \omega, \mathrm{d}\eta
\rangle_{L^2\Lambda^{k}(\Omega)} = 0, \ \forall \eta \in \mathring H\Lambda^{k-1}(\Omega) \}
= \{\omega \in H^*\Lambda^k(\Omega) | \delta \omega = 0\}
$$

$$
\{\omega \in L^2\Lambda^k(\Omega) | \langle \omega, \delta \eta
\rangle_{L^2\Lambda^{k}(\Omega)} = 0, \ \forall \eta \in \mathring H\Lambda^{k+1}(\Omega) \}
= \{\omega \in H\Lambda^k(\Omega) | \mathrm{d} \omega = 0\}
$$

$$
\mathring{\mathfrak{H}}^k = \{\omega \in \mathring H\Lambda^k(\Omega) \cap H^*\Lambda^k
(\Omega) | \mathrm{d} \omega = 0, \delta \omega =0\}
$$

<p style="color:red"><b>以上三个结论需要证明</b></p>

显然有: $$ \mathring{\mathfrak{H}}^{n-k}(\Omega) = \star \mathfrak{H}^k(\Omega)$$

## **同调代数**
同调代数将微分几何中的 $$ \mathrm{de Rham}$$
上同调和代数拓扑中的单纯形同调结合起来，再很多种数学分支中都有应用.
这里将会给出基本定义, 如上链映射, 上链投影和上链同伦.

**上链复形**: 一个上链复形由一列向量空间(或者交换群)和一系列映射组成:

$$
\dots \to V_{k-1} \xrightarrow{d_{k-1}} V_k \xrightarrow{d_{k}} V_{k+1} \to
\dots
$$

其中 $${\rm d}_{k+1}\circ \mathrm{d}_{k} = 0$$, 即称 $$V = \oplus V_{k}$$
和次数加 $$1$$ 的映射 $${\rm d} : V \to V$$, 
$${\rm d}_{k+1}\circ \mathrm{d}_{k} = 0$$ 为上链复形 $$(V, \mathrm{d})$$ .
 
**注意:** 在有限元分析中讨论的复形, 当 $$k < 0$$ 或 $$k$$ 足够大时, $$V_k = 0$$.

记 $$\mathcal{R}( \mathrm{d}_k)$$ 为 $$ \mathrm{d}_k$$ 的像空间, 称为
**k-coboundaries**, $$\mathcal{N}(
\mathrm{d}_k)$$ 为 $$ \mathrm{d}_k$$ 的零空间, 称为 **k-cocycles**. 商空间 $$H^k(V) := \mathcal{N}(
\mathrm{d}_k)/\mathcal{R}( \mathrm{d}_{k-1})$$ 是 $$k$$ 次 **上同调空间**.

给出两个上链 $$V, V'$$, 若一列映射 $$f_k: V_k \to V_k'$$ 满足 
$$ \mathrm{d}_k'f_k = f_{k+1} \mathrm{d}_k$$ 则称其为 **上链映射**,
对于一个上链映射 $$f$$, $$f_k$$ 会将 k-cocycles 映射为 k-cocycles, 
将 k-coboundaries 映射为 k-coboundaries, 所以诱导了一个上同调空间间的映射: 
$$H^k(f) : H^k(V) \to H^k(V')$$

若 $$V'$$ 是 $$V$$ 的子链(即 $$V_k' \subset V_k$$), 则恒同映射 $$i : V' \to V$$
是一个上链映射, 同时诱导了一个上同调映射 $$H^k(V') \to H^k(V)$$.




















