---
title: 微分、变分和非线性问题
author: cbtxs
date: 2022-10-31 12:04:14 +0800
katex: true
comments : true
categories: [偏微分方程数值解]
tags: [微分几何, 偏微分方程数值解, 有限元]
---
## 写在前面
变分是一个非常强大的数学工具,
在计算数学理论和算法设计中有很多应用.冯康院士借助变分原理奠定了有限元计算方法的严格数学理论,
为后世有限元计算方法的实际应用提供了理论保证, 是近代中国数学的巨大创新. 

在笔者学习的过程中发现很多资料中只讲了变分的计算,
没有说明计算出来的变分是什么?但是事实上变分就是无穷维Hilbert空间上的微分.
所以本文从微分出发,讲一讲微分与变分之间的联系, 最后使用 FEALPy,
基于变分求解一个非线性抛物方程. 

## 一、微分
>**定义**: 设函数 $$f$$ 为在 $$x_0$$ 邻域有定义的函数, 若存在 $$A \in \mathbb R$$, 使得

>$$\Delta f = f(x_0+\Delta x) - f(x_0) = A \Delta x + O(\Delta x),$$

>则称 $$f$$ 在 $$x_0$$ 处可微, 微分为

>$$\mathrm df = A\mathrm dx.$$

在梅加强版的数学分析中, 将 $$x \to Ax$$ 的线性映射称为 $$f$$ 在 $$x_0$$ 处的微分. 
对于 $$\mathbb R^n$$ 上的函数 $$f$$ 可以类似定义: 

>**定义**: 设函数 $$f$$ 为在 $$\boldsymbol x_0 \in \mathbb R^n$$ 周围有定义的函数, 若存在 $$A \in \mathbb R^n$$ , 使得

>$$\Delta f = f(\boldsymbol x_0+\Delta \boldsymbol x) - f(\boldsymbol x_0) = A \cdot \Delta \boldsymbol x + O(|\Delta \boldsymbol x|),$$

>则称 $$f$$ 在 $$x_0$$ 处可微, 微分为

>$$\mathrm df = A\cdot \mathrm d\boldsymbol x.$$

在梅加强版的数学分析中, 将 $$\boldsymbol x \to A\boldsymbol x$$ 的线性映射称为 $$f$$ 在 $$\boldsymbol x_0$$ 处的微分. 

>**注**: 为什么要说微分 $\mathrm{d}f$ 是一个线性映射呢? 这里引用[1]中的解释:
首先看微分 $$\mathrm{d}f$$ 是做什么用的,  $$\mathrm{d}f$$ 告诉你:
**“我是一个无穷小增量, 你要问增量是多大, 你得给我一个方向 (向量) ,
我告诉你在这个方向上的增量是多少
(实数) ”**, 所以本身微分就是向量到实数的映射. 更多关于这个的讨论见[1]

## 二、变分
对于变分, 常见的定义是这样: 令 $$f \in C^1(\Omega\times\mathbb R\times\mathbb R^{n})$$ , 定义如下泛函:

$$
I(u) = \int_{\Omega} f(x, u(x), \nabla u(x)) \ \mathrm dx.
$$

$$\forall \phi \in C^1_0(\Omega)$$,  $$I$$ 关于 $$\phi$$ 的变分为: 

$$
\delta I(u_0, \phi) = \lim_{t \to 0} \frac{1}{t} (I(u_0+t\phi) - I(u_0)).
$$

这样的定义其实并不好, 因为它只告诉了我们变分如何计算, 但是计算出来的 **“变分”**
是什么? 这个定义就无法回答. 要回答这个问题, 我们还是要回到微分的定义,
从微分出发看变分应该是个什么. 

正如前面所说: 我们希望 $$\mathbb R$$ 上的函数 $$f$$ 的微分存在, 就要存在一个 $$A \in \mathbb{R}$$ , 使得

$$
\Delta f(x_0) = f(x_0+\Delta x) - f(x_0) = A \Delta x + O(\Delta x).
$$

类似的, 对于一个空间 $$V$$ 上的泛函 $$I$$ , 我们可以这样写:

$$
\Delta I(u_0) = I(u_0 + \Delta u) - I(u_0) = A \Delta u + O(\Vert\Delta u\Vert_{V}).
$$

那么问题来了,  $$A$$ 是什么? 是通常的函数么? 很显然不是, 因为 
$$I(u_0 + \Delta u) - I(u_0)$$ 是实数, 那么 $$A\Delta u$$ 也应该是实数, 所以 $$A$$
只能是一个泛函！而且与前面微分的对比,  $$A$$ 还要是一个线性泛函, 定义在 $$V$$ 上.
所以变分应该如下定义. 

>**定义**: 设 $$I$$ 为Banach空间 $$V$$ 上的一个泛函, 若能找到一个线性泛函 $$A$$, 使得:

>$$\Delta I(u_0) = I(u_0 + \Delta u) - I(u_0) = A \Delta u + O(\Vert\Delta u\Vert_{V}).$$

>对于任意的 $$\Delta u \in V$$ 成立, 则称 $$A$$ 是 $$I$$ 在 $$u_0$$ 处的变分, 记为 $$I_{u_0}$$ . 

可以证明变分有以下性质: 

$$
I_{u_0}(v) = \lim_{t \to 0} \frac{I(u_0 + tv) - I(u_0)}{t}, \quad \forall v \in V.
$$

$$V$$ 上的泛函是 $$V$$ 到 $$\mathbb R$$ 上的映射, 更进一步, 对于 $$V$$ 到任意其他 Banach 空间 $$U$$ 上的的映射也可以有类似的定义[2]. 

>**定义**: 设 $$U, V$$ 是两个 Banach 空间, 对于一个算子 $$F : U \to V$$ 若存在一个线性算子
>$$A: U \to V$$ 满足: $$\forall \epsilon > 0, \exists \delta > 0$$ 使得

>$$\Vert F(u) - F(u_0) - A(u - u_0)\Vert_{V} \leq \epsilon \Vert u-u_0\Vert_{U}.$$

>对于任意的 $$||u - u_0|| < \delta$$ 成立, 则称 $$A$$ 是 $$F$$ 在 $$u_0$$ 处的
$$\mathrm{Fr\'echet}$$ 微分, 记为 $F_{u_0}$ 

同样, $$\mathrm{Fr\'echet}$$ 微分也有以下性质: 

$$
F_{u_0}(v) = \lim_{t \to0} \frac{F(u_0 + tv) - F(u_0)}{t}, \quad \forall v \in U.
$$

为了方便叙述, 将 $$\mathrm{Fr\'echet}$$ 微分与变分不加以区分,
将 $$\mathrm{Fr\'echet}$$ 微分也当作变分. 

## 三、牛顿迭代算法
变分应用非常广泛, 像求最速下降曲线方程, 测地线方程等, 很多资料中都有讲, 本文主要讲变分在计算数学中的一个应用: 非线性问题的线性化. 

考虑非线性问题:

$$
\mathcal L(u) = f.
$$

任选初值 $$u_0$$ , 记 $$\mathcal L$$ 在 $$u_0$$ 处的变分为 $$\mathcal L_{u_0}$$ , 令 $$\delta u_0 = u - u_0$$ , 则有

$$
\mathcal L(u) = \mathcal L(u_0+\delta u_0) = \mathcal L(u_0) + \mathcal L_{u_0}(\delta u_0) + O(\Vert\delta u_0\Vert) = f,
$$

舍去高阶项后得到一个以 $$\delta u_0$$ 为未知量的线性问题:

$$
(1)\quad \quad \mathcal L_{u_0}(\delta u_0) = f - \mathcal L(u_0). 
$$

令 $$u_1 = u_0 + \delta u_0$$ , 就得到一个 $$u$$ 的逼近,  $$u_1$$ 代替 $$u_0$$
重复上面的过程就可以得到一个 $$u_2$$ ,以此类推就能得到一个函数列
$$\{u_k\}_{k=0}^{\infty}$$ , 当 $$\mathcal{L}$$ 满足某些性质 (本文不再展开) 时就有
$$\lim_{k \to\infty} u_k=u$$ , 这就是通过牛顿迭代求解非线性方程的过程. 

## 四、有限元求解非线性抛物方程
现在我们使用上述的牛顿迭代法求解一个非线性抛物方程, 考虑问题: 

$$\begin{cases}
 u_t(\boldsymbol x, t) = \nabla \cdot (a(u)\nabla u) \quad & t > 0, \boldsymbol x  \in \Omega\\
u(\boldsymbol x, t) = 0 & t > 0, \boldsymbol x\in \partial \Omega\\
u(\boldsymbol x, t) = u_0(\boldsymbol x) & t = 0, \boldsymbol x \in \Omega
\end{cases}
$$

其中 $$\Omega = (0, 1)^2$$ 是空间区域,  $$[0, T]$$ 是时间区域,  $$a$$ 是一个
$$H_0^1(\Omega)\to L^2(\Omega)$$ 的算子,  $$a(u) = |\nabla u|^{p-2}$$, $$p
\neq 2$$ 是一个常整数, $$u_0(\boldsymbol x) = \sin(\pi x_0)\sin(\pi x_1)$$ 

### (1) 时间离散
首先时间区域离散, 将 $$[0, T]$$ 分成 
$$\{t_0 = 0, t_1, t_2, …t_k = \frac{kT}{N}, \dots, t_N = T\}$$, 
记 $$u^k = u(x, k)$$ , 得到离散方程:

$$
 u_t^n = \nabla \cdot (a(u^n)\nabla u^n).
$$

记 $$\tau = \frac{T}{N}$$ , 将时间项使用向后欧拉离散, 得到离散格式的方程:

$$
u^n -\tau\nabla \cdot (a(u^n)\nabla u^n) = u^{n-1}.
$$

令
$$
\mathcal{L}(u) = u - \tau\nabla\cdot(a(u)\nabla u)
$$
则 $$\mathcal{L}$$ 是 $$H_0^1(\Omega) \to H_0^1(\Omega)$$ 的算子, 问题重写为求解 $$u^n\in H_{0}^1(\Omega)$$ 使其满足: 

$$
(2)\quad \quad \mathcal{L}(u^n) = u^{n-1}.
$$

### (2) 迭代求解
假设已知第 $$n-1$$ 层的函数 $$u^{n-1}$$ , 要求解

$$
\mathcal L(u^n) = u^{n-1}.
$$

这时有一个困难:  $$\mathcal L$$ 是非线性的, 这里使用上一节讲的牛顿迭代算法,
构造一个函数列 $$\{u_k^{n}\}_{k=0}^{\infty}$$ 来逼近 $$u$$ . 令迭代初值为
$$u_0^n = u^{n-1}$$ , 牛顿迭代 $$(1)$$ 进行的关键是求解 $$\delta u_k \in
H_{0}^1(\Omega), k = 1, 2,...$$ , 使其满足

$$
(3)\quad \quad \mathcal{L}_{u^{n}_k}(\delta u_k) = u^{n-1}-\mathcal L(u^n_k).
$$

这是一个线性方程, 已经可以使用有限元方法求解了, 但是在此之前我们得先计算 $$\mathcal L$$ 的变分 $$\mathcal L_{u}$$ : 

$$
\begin{aligned}
\mathcal L_{u}(\delta u)
& = \lim_{t\to0}\frac{1}{t}(\mathcal L(u+t\delta u)-\mathcal L(u))\\
& = \lim_{t\to0}\frac{1}{t}\{u+t\delta u-\tau\nabla\cdot[a(u+t\delta
    u)\nabla(u+t\delta u)] - u + \tau\nabla\cdot(a(u)\nabla u)\}\\
& = \lim_{t\to0}\frac{1}{t}\{t\delta u -\tau\nabla\cdot[a(u+t\delta u)\nabla
    (t \delta u)]- \tau\nabla\cdot[[a(u+t\delta u)-a(u)]\nabla u]\}\\
& = \delta u-\tau\nabla\cdot[a(u)\nabla \delta u] - 
    \tau\nabla\cdot\big[\lim_{t\to0}\frac{1}{t}[a(u+t\delta u)-a(u)]\nabla
    u\big]\\
    \end{aligned}
$$

其中 $$\lim_{t\to0}\frac{1}{t}[a(u+t\delta u)-a(u)]$$ 是 $$a$$ 在 $$u$$ 处的变分作用于 $$\delta u$$ , 即 $$a_u(\delta u)$$ : 

$$
\begin{aligned}
a_{u}(\delta u)
& = \lim_{t\to0}\frac{1}{t}[a(u+t\delta u)-a(u)]\\ 
& = \lim_{t\to0}\frac{1}{t}[|\nabla (u+t\delta u)|^{p-2}-|\nabla u|^{p-2}]\\
& = \lim_{t\to0} \frac{1}{t}[(\nabla u\cdot\nabla u+2t\nabla u \cdot 
    \nabla \delta u + t^2\nabla\delta u\cdot\nabla \delta u)^{ \frac{p-2}{2}} -
    (\nabla u\cdot\nabla u)^{ \frac{p-2}{2}}]\\
& = (p-2)(\nabla u \cdot \nabla u)^{\frac{p-4}{2}}\nabla u \cdot \nabla \delta{u}\\
& = (p-2)|\nabla u|^{p-4}\nabla u \cdot \nabla \delta{u}\\
\end{aligned}
$$

所以: 

$$\mathcal L_u(\delta u) = \delta u-\tau\nabla\cdot[a(u)\nabla\delta u]-\tau\nabla\cdot(a_u(\delta u)\nabla u)$$.

### (3) 空间离散
令等式 $$(3)$$ 两边乘以测试函数 $$v \in H_{0}^{1}(\Omega)$$ : 

$$
\int_{\Omega} \mathcal L_{u^n_k}(\delta u_k) v \ \mathrm{d}x = \int_{\Omega} u^{n-1}v\ \mathrm{d}x-\int_{\Omega} \mathcal L(u_k^n) v \ \mathrm dx ,
$$

使用分部积分上式转化为: 

$$
\begin{aligned}
& \int_{\Omega}\delta u_k\ v \ \mathrm dx +
\tau \int_{\Omega}a(u^{n}_k)\nabla \delta u_k \cdot \nabla v \ \mathrm dx + 
\tau\int_{\Omega}a_{u^n_k}(\delta u_k)\nabla u^n_k \cdot \nabla v \ \mathrm dx\\
& = \int_{\Omega} u^{n-1}v \ \mathrm{d}x-\int_{\Omega}u_k^n v\ \mathrm dx-\tau\int_{\Omega} \mathcal a(u_k^n)\nabla u_k^n \cdot \nabla v \ \mathrm dx.
\end{aligned}
$$

那么线性问题 $$(3)$$ 转化为: 求解 $$\delta u_k \in H_{0}^1(\Omega)$$,  $$\forall v \in H_{0}^1(\Omega)$$ , 满足上式.

令 $$\mathcal T$$ 是 $$\Omega$$ 的一个网格剖分,
$$V^L(\mathcal T)$$ 是 $$\mathcal T$$ 上的 Lagrange 有限元空间,
那么对应的有限元问题为: 求解 $$u_h \in V^L_0(\Omega)$$ , 
$$\forall v \in V_0^L(\Omega)$$ 满足: 

$$
(4)\quad \quad   
\begin{aligned}
& \int_{\Omega} u_h\ v \ \mathrm dx +
\tau \int_{\Omega}a(u^{n}_k)\nabla u_h \cdot \nabla v \ \mathrm dx + 
\tau\int_{\Omega}a_{u^n_k}(u_h)\nabla u^n_k \cdot \nabla v \ \mathrm dx\\ 
& = \int_{\Omega} u^{n-1}v \ \mathrm{d}x
-\int_{\Omega}u_k^n v\ \mathrm dx-\tau\int_{\Omega} \mathcal a(u_k^n)\nabla u_k^n \cdot \nabla v \ \mathrm dx.
\end{aligned}
$$
### (4) 有限元求解
记 $$\{\phi_i\}_{i=0}^{NS-1}$$ 是 $$V_0^{L}(\mathcal T)$$ 的基函数, 设

$$
u_h = \sum_{i=0}^{NS-1} U_i \phi_i, \ u_k^n = \sum_{i=0}^{NS-1} U_{k, i}^n \phi_i, \ u^n = \sum_{i=0}^{NS-1} U_i^n \phi_i,
$$

$$
M_{ij} = \int_{\Omega} \phi_i\phi_j \ \mathrm dx, \ \  S_{ij} = \int_{\Omega}
a(u_k^n) \nabla \phi_i \cdot \nabla \phi_j, \ \ B_{ij} = \int_{\Omega}
a_{u^n_k}(\phi_j)\nabla u_k^n \cdot \nabla\phi_i \ \mathrm dx.
$$

则有限元问题 $$(4)$$ 转换为了代数方程: 

$$
AU = F,
$$

其中:  $$A = M+\tau S + \tau B, \quad F = MU^{n-1} - MU^{n}_k - \tau SU_k^n$$ 
### (5) 程序实现
程序实现见
[https://github.com/weihuayi/fealpy/tree/master/example/NonLinearParabolic_example.py](https://github.com/weihuayi/fealpy/tree/master/example/NonLinearParabolic_example.py)

## 五、总结
$$\mathbb R^n$$ 空间上函数的微分, 与函数空间上算子的变分, 不同的概念却有着深刻的联系,
以至于原本应用于 $$\mathbb R^n$$ 上的牛顿迭代也可以处理函数空间上的非线性问题,
这就是数学的魅力, 
这种和谐统一, 这种一步步抽象后俯瞰问题本质的感觉正是数学最吸引我们的地方. 

## 六、参考文献
- [1]梁灿彬, 周彬. 微分几何入门与广义相对论.上册.第2版[M]. 科学出版社, 2009.
- [2][$$\mathrm{Fr\'echet derivative}$$](https://en.wikipedia.org/wiki/Fr%C3%A9chet_derivative)
