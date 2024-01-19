---
title: 不等式(一)：基本不等式 
author: cbtxs
date: 2022-04-29 20:30:52 +0800
katex: true
comments : true
categories: [偏微分方程数值解]
tags: [偏微分方程, 偏微分方程数值解]
---

## **写在前面** 
不等式在偏微分方程数值解的误差分析中有至关重要的作用, 本文记录常用的一些不等式,
其中都是 evins 的《偏微分方程》这本书中的不等式.

## **常用不等式**
1. **Cauchy 不等式**

   $$
   ab \leq \frac{a^2}{2} + \frac{b^2}{2} \quad (a, b \in \R)
   $$

   **证明:** $$\ a^2+b^2 -2ab \geq 0$$
2. **Young 不等式:** 若 $$1 < p, q < +\infty$$, $$\frac{1}{p} + \frac{1}{q}=1$$,
   则:

   $$
   ab \leq \frac{a^p}{p} + \frac{b^q}{q} \quad (a, b > 0)
   $$

   **证明:** 映射 $$x \to e^x$$ 是凸的, 即:

   $$
   e^{\lambda a + (1-\lambda)b} \leq \lambda e^a + (1-\lambda)e^b 
   $$

   所以:

   $$
   ab = e^{ \frac{1}{p}\ln a^p + \frac{1}{q}\ln b^q} \leq 
   \frac{e^{\ln a^p}}{p}  + \frac{e^{\ln b^q}}{q} = \frac{a^p}{p} + \frac{b^q}{q}
   $$
3. **Holder 不等式(积分形式):** 若 $$1 < p, q < +\infty$$, $$\frac{1}{p} + \frac{1}{q}=1$$,
$$u \in L^p(U), v \in L^q(U)$$, 则:

   $$
   \int_{U} |uv| \ \mathrm dx \leq ||u||_{L^p(U)} ||v||_{L^q(U)}
   $$

   **证明:** 令 $$\hat u = \frac{u}{ \lVert u \rVert_{L^p(U)}}, \hat v =
   \frac{v}{ \lVert v \rVert_{L^q(U)}}$$, 则 $$ \lVert \hat u \rVert_{L^p(U)} =
   1, \lVert \hat v \rVert_{L^q(U)} = 1$$, 所以: 
   
   $$
   \begin{aligned}
   \int_{U} |uv| \ \mathrm dx 
   & = \lVert u \rVert_{L^p(U)} \lVert v \rVert_{L^q(U)}
     \int_{U}|\hat u\hat v| \ \mathrm dx\\ 
   & \leq \lVert u \rVert_{L^p(U)} \lVert v \rVert_{L^q(U)}
     \left(\frac{1}{p}\int_{U} |\hat u|^p \mathrm dx +
     \frac{1}{q} \int_{U} |\hat v|^{q}\mathrm dx\right)\\
   & = \lVert u \rVert_{L^p(U)} \lVert v \rVert_{L^q(U)}
   \end{aligned}
   $$
4. **Holder 不等式(离散形式):** 

   $$
   |\sum_{k=1}^n a_k b_k| \leq \left(\sum_{k=1}^n |a_k|^p\right)^{ \frac{1}{p}}
    \left(\sum_{k=1}^n |b_k|^q\right)^{ \frac{1}{q}}
   $$

   **证明：** 略.

5. **一般的 Hodler 不等式：** 若 $$1 < p_1, \cdots, p_n < +\infty$$, 
   $$\frac{1}{p_1} + \cdots + \frac{1}{p_n}=1$$, $$u_i \in L^{p_i}(U)$$, 则

   $$
   \int_{U} |u_1 u_2 \cdots u_n| \ \mathrm dx \leq \prod_{i=1}^n||u_i||_{L^{p_i}(U)}
   $$

   **证明：** 略.
6. **Minkowski 不等式**: 若 $$1 \leq p < \infty$$, $$u, v \in L^p(U)$$, 则:

   $$
   \lVert u+v \rVert_{L^p(U)} \leq \lVert u \rVert_{L^p(U)} + \lVert v
   \rVert_{L^p(U)}
   $$

   **证明:** 

   $$
   \begin{aligned}
       \lVert u+v \rVert_{L^p(U)}^p 
       & = \int_{U}|u+v|^p \ \mathrm dx \\
       & \leq \int_{U}|u+v|^{p-1}(|u|+|v|)\ \mathrm dx\\
       & = \int_{U}|u+v|^{p-1}|u|\ \mathrm dx + \int_{U}|u+v|^{p-1}|v|\ \mathrm dx\\
       & \leq \left(\int_{U} |u+v|^p \ \mathrm dx \right)^{ \frac{p-1}{p}}
       \left(
       \left(\int_{U} |u|^p \ \mathrm dx\right)^{ \frac{1}{p}} + 
       \left(\int_{U} |v|^p \ \mathrm dx\right)^{ \frac{1}{p}}
       \right)\\
       & = \lVert u+v \rVert_{L^p(U)}^{p-1} 
           \left(\lVert u \rVert_{L^p(U)}+ \lVert v \rVert_{L^p(U)}\right)
   \end{aligned}
   $$
7. **Minkowski 不等式**(离散形式):

   $$
   \left(\sum_{k=1}^n |a_k + b_k|^p\right)^{\frac{1}{p}} \leq 
   \left(\sum_{k=1}^n |a_k|^p\right)^{\frac{1}{p}} + 
   \left(\sum_{k=1}^n |b_k|^p\right)^{\frac{1}{p}}
   $$

   **证明：** 略.

8. **$$L^p$$ 范数的插值不等式** 若 $$1 \leq s \leq r \leq t \leq +\infty, \ u 
   \in L^s(U) \cap L^t(U)$$, 且:

   $$
   \frac{1}{r} = \frac{\theta}{s} + \frac{(1-\theta)}{t}
   $$

   那么有:

   $$
   \lVert u \rVert_{L^r(U)} \leq 
   \lVert u \rVert_{L^s(U)}^\theta \lVert u \rVert_{L^t(U)}^{1-\theta}
   $$

   **证明:** 令 $$g = |u|^r, p = \frac{s}{\theta r}, 
   q = \frac{t}{(1-\theta) r}$$, 则 $$\frac{1}{p} + \frac{1}{q} = 1$$:

   $$
   \begin{aligned}
       \|u\|_{L^r(u)}^r = 
       \int_{U} |g| \ \mathrm dx & \leq \int_{U} |g|^{\theta} |g|^{1-\theta} 
       \ \mathrm dx\\
       & \leq \left(\int_{U} |g|^{\theta p}\ \mathrm dx \right)^{\frac{1}{p}} 
            \left(\int_{U} |g|^{(1-\theta) q}\ \mathrm dx
            \right)^{\frac{1}{q}}\\
       & = \left(\int_{U} |u|^{s}\ \mathrm dx \right)^{\frac{\theta r}{s} } 
            \left(\int_{U} |u|^{t}\ \mathrm dx
            \right)^{\frac{(1-\theta)r}{t}}\\
       & = \lVert u \rVert_{L^s(U)}^{\theta r}
           \lVert u \rVert_{L^t(U)}^{(1-\theta) r}
   \end{aligned}
   $$

9. **Gronwall 不等式(微分形式)**: 若 $$\eta(t)$$ 在 $$[0, T]$$ 上非负且绝对连续,
   $$\phi, \psi$$ 在 $$[0, T]$$ 上非负可积, 且在 $$[0, T]$$ 上几乎处处有:

   $$
   \eta'(t) \leq \phi(t)\eta(t) + \psi(t)
   $$

   则

   $$
   \eta(t) \leq e^{\int_0^t \phi(s) \ \mathrm ds}
   \left(
   \eta(0) + \int_0^t \psi(s) \ \mathrm ds
   \right)
   $$

   **证明:** 

   $$
   \frac{d}{ds} \left(\eta(s) e^{-\int_0^s \phi(r) \ \mathrm dr}\right)
   = (\eta'(s) - \eta(s) \phi(s)) e^{-\int_0^s \phi(r) \ \mathrm dr}
   \leq \psi(s) e^{-\int_0^s \phi(r) \ \mathrm dr} \leq \psi(s)
   $$

   上式子几乎处处成立, 左右两边在 $$[0, t]$$ 作积分有:

   $$
    \eta(t) e^{-\int_0^t \phi(r) \ \mathrm dr} \leq \eta(0) + \int_0^t \psi(t) \
    \mathrm dt
   $$

   证明结束.

   **注意:** 当 $$\psi = 0, \eta(0) = 0$$, 则 $$\eta == 0$$
9. **Gronwall 不等式((积分形式)**: 若 $$u(t)$$ 是 $$[0, T]$$ 上一个非负可积函数, 几乎处处满足:

   $$
   u(t) \leq C_1 \int_0^t u(s) \ \mathrm ds + C_2
   $$

   则:

   $$
   u(t) \leq C_2(1 + C_1 t e^{C_1 t})
   $$

   **证明:** 令 $$\eta(t) = \int_0^t u(s) \ \mathrm ds$$, 则可以用微分形式的
   Gronwall 不等式证明.

## 偏微分方程中的不等式
1. **$$\mathrm{Poincar\'e}$$ 不等式:** 令 $$U$$ 是一个 $$R^n$$ 中的有界连通开集,
   边界 $$C^1$$ 光滑, 那么存在只与 $$n, U$$ 有关的常数 $$C$$, 使得:

   $$
   ||u - (u)_U||_{L^2(U)} \leq C||Du||_{L^2(U)}
   $$

   其中 $$(u)_U = \frac{1}{\|U\|}\int_{U} u \mathrm dx$$.

2. **$$\mathrm{Poincar\'e}$$ 不等式:** 令 $$U$$ 是一个 $$R^n$$ 中的有界连通开集,
   边界 $$C^1$$ 光滑, 若 $$u \in H^1_0(U)$$ 那么存在只与 $$n, U$$ 
   有关的常数 $$C$$, 使得:

   $$
   ||u||_{L^2(U)} \leq C||Du||_{L^2(U)}
   $$









