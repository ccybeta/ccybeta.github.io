---
title: Green's function 
author: cbtxs
date: 2022-06-21 11:02:14 +0800
katex: true
comments : true
categories: [偏微分方程数值解]
tags: [偏微分方程, 偏微分方程数值解]
---

## **Poisson 方程的格林函数**
考虑问题:

$$
\begin{cases}
    -\Delta u = f \quad \text{in} \ \Omega\\
    u = g \quad \text{on} \ \partial \Omega
\end{cases}
\qquad \qquad (1)
$$

$$\Omega \in \mathbb R^3$$. 假设 $$G(x)$$ 满足:

$$
\begin{cases}
    -\Delta G = \delta_0 \quad \text{in} \ \Omega\\
    G = 0 \quad \text{on} \ \partial \Omega
\end{cases}
\qquad \qquad (2)
$$

则有: 

$$
\begin{aligned}
u(x) & = \int_{\Omega} \delta_x u(y) \ \mathrm dy\\
& = -\int_{\Omega} \Delta G(y-x) u(y) \ \mathrm dy\\
& = \int_{\Omega} \nabla G(y-x) \nabla u(y) \ \mathrm dy
 - \int_{\partial \Omega} u(y)\nabla G(y-x) \cdot \boldsymbol n \ \mathrm dS\\
& = \int_{\partial \Omega} G(y-x) \nabla u(y) \cdot \boldsymbol n -
\int_{\Omega} \Delta u(y) G(y-x) \ \mathrm dy\\
& \quad \quad - \int_{\partial \Omega} u(y)\nabla G(y-x) \cdot \boldsymbol n \ \mathrm dS\\
& = -\int_{\Omega} f(y)G(y-x) \ \mathrm dy - \int_{\partial \Omega} g\nabla
G(y-x)\cdot \boldsymbol n \ \mathrm dS
\end{aligned} 
$$

所以只要我们能解出问题 (2) 中的 $$G(y)$$ 那么对于任意的 $$L^1$$ 函数 $$f, g$$
都可以用上面的公式解决问题 (1), 其中 $$G$$ 被称为是方程(1)的格林函数.

### 特殊区域的格林函数
1. **$$R^3$$ 上的格林函数:** 对问题 (2) 第一项左右同时傅里叶变换:

    $$
    -\hat{\Delta G} = \hat{\delta_0} \quad \Rightarrow \quad 
    |\boldsymbol{k|}^2 \hat{G} = 1 \quad \Rightarrow \hat{G} = \frac{1}{|\boldsymbol{k}|^2}
    $$

    所以:

    $$
    \begin{aligned}
        G(\boldsymbol{x}) & = -\frac{1}{(2\pi)^3}\int_{R^3} \frac{1}{|\boldsymbol{k}|^2} 
        e^{i \boldsymbol{k}\cdot \boldsymbol{x}} \ \mathrm d \boldsymbol{k}\\
        & = -\frac{1}{(2\pi)^3}\int_{0}^{+\infty} \int_{0}^{2\pi} \int_{0}^{\pi} \frac{1}{r^2} e^{i
        r\cos(\phi)| \boldsymbol{x}|} r^2\sin(\phi)
        \mathrm d \phi \mathrm d \theta \mathrm dr\\
        &= -\frac{1}{(2\pi)^2} \int_{0}^{+\infty} 
        \left(\int_{0}^{\pi} e^{ir\cos(\phi)|x|}
        \mathrm d\cos(\phi)\right) \mathrm dr\\
        & = -\frac{1}{2\pi^2| \boldsymbol{x}|} \int_{0}^{+\infty} \frac{\sin(r| \boldsymbol{x}|)}{r} \mathrm dr\\
        & = -\frac{1}{4\pi | \boldsymbol{x}|}

    \end{aligned}
    $$



## **Helmholtz 方程的格林函数**
考虑问题:

$$
\begin{cases}
    \Delta u + \omega^2 u = f \quad \text{in} \ \Omega\\
    u = g \quad \text{on} \ \partial \Omega
\end{cases}
\qquad \qquad (3)
$$

$$\Omega \in \mathbb R^3$$. 假设 $$G(x)$$ 满足:

$$
\begin{cases}
    \Delta G + \omega^2 G = \delta_0 \quad \text{in} \ \Omega\\
    G = 0 \quad \text{on} \ \partial \Omega
\end{cases}
\qquad \qquad (4)
$$

称 $$G$$ 是 方程(3) 的格林函数.

### 特殊区域的格林函数
1. **$$R^3$$ 上的格林函数:** 对问题 (2) 第一项左右同时傅里叶变换:

    $$
    \hat{\Delta G} + \omega^2 \hat{G} = \hat{\delta_0} \quad \Rightarrow \quad 
    (\omega^2-|\boldsymbol{k|}^2) \hat{G} = 1 \quad 
    \Rightarrow \hat{G} = \frac{1}{\omega^2-|\boldsymbol{k}|^2}
    $$

    所以:

    $$
    \begin{aligned}
        G(\boldsymbol{x}) & = \frac{1}{(2\pi)^3}\int_{R^3} 
        \frac{1}{\omega^2-|\boldsymbol{k}|^2} 
        e^{i \boldsymbol{k}\cdot \boldsymbol{x}} \ \mathrm d \boldsymbol{k}\\
        & = \frac{1}{(2\pi)^3}\int_{0}^{+\infty} 
        \int_{0}^{2\pi} \int_{0}^{\pi} \frac{1}{\omega^2-r^2} e^{i
        r\cos(\phi)| \boldsymbol{x}|} r^2\sin(\phi)
        \mathrm d \phi \mathrm d \theta \mathrm dr\\
        &= -\frac{1}{2(2\pi)^2} \int_{0}^{+\infty}\left(\frac{r}{\omega+r} +
        \frac{r}{r-\omega}\right)
        \left(\int_{0}^{\pi} e^{ir\cos(\phi)|x|}
        \mathrm d\cos(\phi)\right) \mathrm dr\\
        & = -\frac{1}{8\pi^2| \boldsymbol{x}|} 
        \int_{-\infty}^{+\infty} 
        \frac{\sin(r| \boldsymbol{x}|)}{\omega + r} \mathrm dr+
        \int_{-\infty}^{+\infty} 
        \frac{\sin(r| \boldsymbol{x}|)}{r - \omega} \mathrm dr\\
        & = -\frac{1}{4\pi^2 | \boldsymbol{x}|} \int_{-\infty}^{+\infty} 
        \frac{\sin(r| \boldsymbol{x}|)\cos(\omega |\boldsymbol{x}|)}{r} 
        \ \mathrm dr\\
        & = -\frac{1}{4\pi |\boldsymbol{x}|}\cos(\omega| \boldsymbol{x}|)

    \end{aligned}
    $$












