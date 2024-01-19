---
title: Cuthill-Mckee 算法
author: cbtxs
date: 2022-06-08 11:02:14 +0800
mathjax: true
pseudocode: true
comments : true
categories: [高性能计算]
tags: [偏微分方程, 偏微分方程数值解, 编程, 高性能计算]
---

## **写在前面**
如何高效的求解矩阵方程是计算数学中的核心问题, 在大多数偏微分方程数值方法中, 
需要计算的矩阵是稀疏矩阵. 稀疏矩阵有一个 **带宽** 的概念: 
**一个矩阵某一行的第一个非零元位置到最后一个非零元的距离称为这一行的带宽,
矩阵最大行带宽就是矩阵的带宽**. 为了能够快速求解, 一般希望矩阵的带宽越小越好. 
Cuthill-Mckee 算法就是一种降低矩阵带宽的算法.

$$
\begin{pmatrix}
  1 & 0 & 0 & 1 & 1 & 0 & 0 & 0\\
  0 & 1 & 1 & 0 & 1 & 0 & 0 & 0\\
  0 & 1 & 1 & 0 & 0 & 0 & 0 & 0\\
  1 & 0 & 0 & 1 & 0 & 0 & 0 & 0\\
  1 & 0 & 0 & 0 & 1 & 0 & 0 & 1\\
  0 & 1 & 0 & 0 & 0 & 1 & 0 & 0\\
  0 & 0 & 0 & 0 & 0 & 0 & 1 & 0\\
  0 & 0 & 0 & 0 & 1 & 0 & 0 & 1\\
\end{pmatrix}
$$

## **矩阵方程角度的降低带宽**

对于一个矩阵方程:

$$
Ax = b
$$

若 $$P$$ 是一个循环矩阵则:

$$
P^TAPP^Tx = P^T b
$$

与原方程同解, 令 $$B = P^TAP, y = P^Tx, c = P^T c$$, 则求解

$$
By = c
$$

后, 令 $$x = Py$$ 则得到原方程的解. 而使用合适的循环矩阵 $$P$$ 可以使 $$B$$
的带宽小与 $$A$$ 的带宽, 所以寻找合适的 $$P$$ 就是降低带宽的关键.

## **网格角度的降低带宽**
在有限元方法中, 组装的矩阵实际上是自由度的 **邻接矩阵**,
如对于质量矩阵 $$M$$, 只有当 2, 3 号自由度在同一个单元时, $$M(2, 3)$$
才有可能不为 0, 不在一个单元时 $$M(2, 3)$$ 一定为 0. 

$$
M = 
\begin{pmatrix}
\frac{1}{12} & \frac{1}{24} & \frac{1}{24} & \frac{1}{24}\\
\frac{1}{24} & \frac{1}{12} & \frac{1}{12} & \frac{1}{12}\\
\frac{1}{24} & \frac{1}{24} & \frac{1}{12} & 0\\
\frac{1}{24} & \frac{1}{24} & 0 & \frac{1}{12}\\
\end{pmatrix} \quad 
M = 
\begin{pmatrix}
\frac{1}{12} &  0 & \frac{1}{24} & \frac{1}{24}\\
0 & \frac{1}{12} & \frac{1}{12} & \frac{1}{12}\\
\frac{1}{24} & \frac{1}{24} & \frac{1}{12} & \frac{1}{24}\\
\frac{1}{24} & \frac{1}{24} & \frac{1}{24} & \frac{1}{12}\\
\end{pmatrix}
$$

那么显然, **矩阵 $$A$$ 在第
$$k$$ 行的带宽就是与第 $$k$$ 个自由度相邻的自由度中最大编号与最小编号之差**. 
前面的 $$P^TAP$$ 实际上表示对自由度从新编号后的邻接矩阵.
记自由度集合为 $$\mathcal D$$, 降低带宽问题等价于: **求一种自由度的编号规则,
使自由度的邻接矩阵带宽讲到最低.**

## **Cuthill-Mckee 算法**
Cuthill-Mckee 算法就是一种根据邻接矩阵给自由度编号的算法, 算法如下:

<pre id="Cuthill-Mckee" class="pseudocode" style="display:hidden;">
\begin{algorithm}
        \caption{Cuthill-Mckee}
        \begin{algorithmic}
        \INPUT 邻接矩阵 n2n
        \OUTPUT 优化带宽的自由度顺序数组 order
        \STATE 计算网格中所有点的度 degree.
        \STATE 给最小度节点 v 编 0 号, 即 order[v] = 0.
        \STATE 记有序集合 R = \{v\}, k = 1 
        \WHILE{R $\neq \emptyset$}
          \STATE 取 R 的头部元素, 记为 x.
          \STATE 找到与 x 相邻且没有编号的点的集合 $S$.
          \STATE 对 $S$ 中的点按度的大小从小到大的排序
          \FOR{y $\in$ S}
            \STATE 给 y 编号 k, 即 order[y] = k
            \STATE 将 y 插入 R 的尾部.
            \STATE k++
          \ENDFOR
        \ENDWHILE
        \END{ALGORITHMIC}
        \END{ALGORITHM}
</pre>

<script>
    pseudocode.renderElement(document.getElementById("Cuthill-Mckee"));
</script>

## **Reverse-Cuthill-Mckee 算法**
Cuthill-Mckee 算法实际上就是选取了一个点 $v$, 然后距离他为 1 的点记为第一圈, 为
2 的点记为第二圈的点, 第 $k$ 圈的点编号永远小于第 $k+1$ 圈的点的编号.
所以只要每一圈的点个数越少, 那么带宽就越小. 

如下图:

所以 Cuthill-Mckee 算法第一个点的选取会影响带宽的大小, 但是如果能找到一个点,
使得距离他的 "圈数" 很多, 那么就变相的可以认为每圈的元素个数很少.
下面是找到这样的点的算法:

<pre id="Cuthill-Mckee" class="pseudocode" style="display:hidden;">
\begin{algorithm}
        \caption{Deepth}
        \begin{algorithmic}
        \INPUT 邻接矩阵 n2n, 节点 v
        \OUTPUT 以 v 为起点的深度 d, 最长的树 T
        \STATE 用 R 表示第 d 圈的节点, R = \{v\}
        \STATE 记 v$'$ = v, T = \{v\}, d = 1
        \WHILE{R $\neq \emptyset$}
          \STATE 找到与 R 相邻的且没有计算与 v 的距离的点集 S
          \STATE 找到一个 S 中与 v$'$ 相连的点 v$''$, 将 v$''$ 放入 T
          \STATE 更新数据 d++, v$'$ = v$''$, R = S 
        \ENDWHILE
        \END{ALGORITHMIC}
        \END{ALGORITHM}
</pre>


<pre id="Cuthill-Mckee1" class="pseudocode" style="display:hidden;">
\begin{algorithm}
        \caption{Reverse-Cuthill-Mckee}
        \begin{algorithmic}
        \INPUT 邻接矩阵 n2n
        \OUTPUT 优化带宽的自由度顺序数组 order
        \STATE 任选一点 v.
        \WHILE{True}
        \STATE 使用 Deepth 算法计算 v 的深度 d0, 最长树 T.
        \STATE 选择 T 中度最小的点 v$'$, 使用 Deepth 算法计算其深度 d1, 最长树 T1.
        \IF{d1 > d0}
          \STATE v = v$'$
        \ELSE
          \STATE \BREAK
        \ENDIF
        \ENDWHILE
        \STATE 以 v 为起点使用 Cuthill-Mckee 算法
        \END{ALGORITHMIC}
        \END{ALGORITHM}
</pre>

<script>
    pseudocode.renderElement(document.getElementById("Cuthill-Mckee"));
</script>


<script>
    pseudocode.renderElement(document.getElementById("Cuthill-Mckee1"));
</script>














