---
title: 数学知识随记
author: cbtxs
date: 2022-05-10 14:50:14 +0800
katex: true
comments : true
categories: [其他]
tags: [数学]
---

## 写在前面
因为以前没有做笔记的习惯, 导致自己学了很多东西现在都忘记了,
想要从新捡起来无从下手, 所以本文就记录一下平时学到的数学概念和知识,
方便以后查阅.

## 泛函分析
1. **距离空间的完备化:**  一个距离空间 $$(X, d)$$, 记:

    $$
    \mathcal E = \{\{x_n\}_{n>0} \subset X| \{x_n\}_{n>0}\text{是} (X, d) \text{中的 Cauchy 列}\}
    $$

    定义 $$\mathcal E$$ 的等价关系 $$ \sim : \{x_n\} \sim \{y_n\}$$ 当且仅当 

    $$
    \lim_{n\to \infty} d(\{x_n\}, \{y_n\}) = 0
    $$

    记 $$\bar X = \mathcal E/\sim$$, 距离定义为 $$\bar d$$: 

    $$
    \bar d([\{x_n\}], [\{y_n\}]) = \lim_{n\to \infty} d(x_n, y_n)
    $$

    则 $$(\bar X, \bar d)$$ 是一个完备空间, 在映射 

    $$
    \begin{aligned}
      \Phi: X & \to \bar X\\
            x & \to \{x_n = x\}_{n>0}
    \end{aligned}
    $$

    的意义下, $$(X, d)$$ 等距嵌入于 $$(\bar X, \bar d)$$,
    $$(\bar X, \bar d)$$ 是 $$(X, d)$$ 的完备化.




















