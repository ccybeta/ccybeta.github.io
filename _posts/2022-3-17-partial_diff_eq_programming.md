---
title: 偏微分方程数值解编程
author: cbtxs
date: 2022-03-17 11:02:14 +0800
katex: true
comments : true
categories: [偏微分方程数值解]
tags: [偏微分方程, 偏微分方程数值解, 编程]
---

## **写在前面**
有很多学偏微分方程数值解的同学, 理论学的很好, 算法收敛性, 稳定性会证明,
就是不能把算法编出来, 不会编程的一个原因是没有一门熟悉的编程语言,
另一个很重要的原因是拿到一个算法, 不知道该怎么下手. 
这篇文章的目的就是要解决这个问题, 希望大家读完这篇文章会有所收获.

## **二元一次方程**
首先来看一个初中就学过的鸡兔同笼问题: 
***有若干只鸡兔同在一个笼子里, 从上面数, 有35个头, 从下面数, 有94只脚. 
问笼中各有多少只鸡和兔?***

这个问题的未知量是鸡的个数和兔的个数, 分别设为 $$x, y$$, 那么就可以列出下面方程:

$$
\begin{cases}
x + y = 35\\
2x + 4y = 94
\end{cases}
$$

使用初中知识就可很快解决, 
现在尝试让电脑来解决这个问题, 使用线代知识可以把这个方程写成矩阵形式:

$$
\boldsymbol A \boldsymbol X = \boldsymbol b
$$

其中 

$$
\boldsymbol A = 
\begin{pmatrix}
1 & 1\\
2 & 4
\end{pmatrix}
, \quad
\boldsymbol X = 
\begin{pmatrix}
x \\
y 
\end{pmatrix}
, \quad
\boldsymbol b = 
\begin{pmatrix}
35 \\
94 
\end{pmatrix}
$$

把 $$\boldsymbol A$$ 和 $$\boldsymbol b$$ 输入进电脑, 调用求解器就可以计算出
$$x, y$$. 这看似简单的流程其实包含了大部分的偏微分方程数值解的步骤.

## **五点差分方法**
下面用五点差分求解如下的 Poisson 方程

$$
\begin{cases}
-\Delta u = f \quad in\ \Omega\\
\quad \ \ \   u = 0 \quad on\ \partial \Omega
\end{cases}
$$

***其中 $$f = sin(x)sin(y),\ \Omega = [0, \pi]\times[0, \pi]$$***.

将 $$\Omega$$ 离散为以下网格:

<div align='center'>
<img src = "../../image/5d.svg" width=250>
</div>

现在按上面求解二元一次方程的方法编写五点差分程序求解这个 Poisson 方程. 

首先第一步, 我们的未知量是什么? 是网格中每个节点处的值, 用 $$u_{ij}$$
表示第 $$i$$ 列, 第 $$j$$ 行的节点 $$(x_i, y_j)$$ 处 $$u$$ 的函数值.
使用五点差分格式离散 $$\Delta u$$

$$
\begin{align*}
\Delta u(x_i, y_j) & = u_{xx}(x_i, y_j) + u_{yy}(x_i, y_j) \\
                   & \approx
\frac{u_{i+1, j}+u_{i-1, j}-2u_{i,j}}{h_0^2}
+ \frac{u_{i, j+1}+u_{i, j-1}-2u_{i,j}}{h_1^2}
\end{align*}
$$

其中 $$h_0, \ h_1$$ 是 $$x, \ y$$ 方向的步长.
有了这个结果我们就可以列方程了:

$$
\begin{cases}
\frac{u_{i+1, j}+u_{i-1, j}-2u_{i,j}}{h_0^2}
+ \frac{u_{i, j+1}+u_{i, j-1}-2u_{i,j}}{h_1^2}
= f(x_i, y_j) \quad (x_i, y_j) \in \Omega\\
u(x_i, y_j) = 0 \quad (x_i, y_j) \in \partial \Omega
\end{cases}
$$

其中第一个类型的方程有 9 个, 第二个方程的个数有 25 - 9 = 16 个,
现在把他写成矩阵形式:

$$
AX = b
$$

这个时候, 很多人会觉得这个式子中最先获得的是 $$A$$, 但事实上, 
我们最先做的应该是确定 $$X, b$$, 只有把未知量 $$X$$ 和右端项 $$b$$ 
的顺序确定才能确定出 $$A$$.

确定 $$X$$:

$$
X = 
\begin{pmatrix}
u_{0,0}\\
u_{0,1}\\
\vdots\\
u_{1,0}\\
u_{1,1}\\
\vdots\\
u_{4,4}
\end{pmatrix}, \quad
b = 
\begin{pmatrix}
f_{0,0}\\
f_{0,1}\\
\vdots\\
f_{1,0}\\
f_{1,1}\\
\vdots\\
f_{4,4}
\end{pmatrix}
$$

即: 

$$
X_i = u_{i \% 5, i/5}, b_i = f_{i\%5, i/5}
$$

重写方程:

$$
\begin{cases}
\frac{1}{h_0^2}X_{i*5+5+j} + \frac{1}{h_0^2}X_{i*5 - 5 + j} 
- 2(\frac{1}{h_0^2} + \frac{1}{h_1^2})X_{i*5 + j} + 
\frac{1}{h_1^2}X_{i*5+j+1} + \frac{1}{h_0^2}X_{i*5 + j-1} 
= b_{i*5+j}, \quad 0 < i, j < 4\\
X_{i*5+j} = 0. \quad i, j \in \{0, 4\}
\end{cases}
$$

$$i = i*5+j$$ 即:

$$
\begin{cases}
\frac{1}{h_0^2}X_{i+5} + \frac{1}{h_0^2}X_{i - 5} 
- 2(\frac{1}{h_0^2} + \frac{1}{h_1^2})X_{i} + 
\frac{1}{h_1^2}X_{i+1} + \frac{1}{h_0^2}X_{i-1} 
= b_{i}, \quad 0 < i \% 5, i/5 < 4\\
X_{i} = 0. \quad i\%5, i/5 \in \{0, 4\}
\end{cases}
$$

所以 矩阵 $$A: (25, 25)$$:
- 若 $$0 < i \% 5, i/5 < 4 :$$

$$
A_{i, j} = 
\begin{cases}
\frac{1}{h_0^2}, \quad j = i+5 \ or\ j = i-5\\
\frac{1}{h_1^2}, \quad j = i-1 \ or\ j = i+1\\
- 2(\frac{1}{h_0^2} + \frac{1}{h_1^2}), \quad j = i
\end{cases}
, \quad
A_{ij} = \delta_{ij}
$$

- 若 $$i\%5 \in \{0, 4\}\ or\ i/5 \in \{0, 4\} :$$

$$
A_{ij} = \delta_{ij}
$$

```python
import numpy as np
import copy
import scipy.linalg

def f(x,y):
    z=np.cos(3*x)*np.sin(np.pi*y)
    return -z
#真解
def zj(x,y):
    z=np.cos(3*x)*np.sin(np.pi*y)/(9+np.pi**2)
    return z

n=int(input('n='))

a,b=0,np.pi
c,d=0,1

h1=(b-a)/n
h2=(d-c)/n
xdate=np.linspace(a,b,n+1)
ydate=np.linspace(c,d,n+1)
A=np.zeros([(n+1)**2,(n+1)**2])
for i in range(n+1):
    if i==0:
        for j in range(n+1):
            A[j,j]=1
    elif i==n:
        for j in range(n+1):
            A[n*(n+1)+j,n*(n+1)+j]=1
    else:
        A[i*(n+1),i*(n+1)]=1
        A[(i+1)*(n+1)-1,(i+1)*(n+1)-1]=1
        for j in range(n+1)[1:-1]:
            A[i*(n+1)+j,i*(n+1)+j]=-2/h1**2-2/h2**2
            A[i*(n+1)+j,i*(n+1)+j-1]=1/h2**2
            A[i*(n+1)+j,i*(n+1)+j+1]=1/h2**2
            A[i*(n+1)+j,(i-1)*(n+1)+j]=1/h1**2
            A[i*(n+1)+j,(i+1)*(n+1)+j]=1/h1**2
x_0,y_0=np.meshgrid(xdate[1:-1],ydate[1:-1])
F=np.zeros([n+1,n+1])
F[1:-1,1:-1]=f(x_0,y_0)
F[:,0]=zj(0,ydate)
F[:,-1]=zj(np.pi,ydate)
F=F.T
F=F.flatten()
u=np.linalg.solve(A,F)
u=u.reshape(n+1,n+1)
x_1,y_1=np.meshgrid(xdate,ydate)
kkk=zj(x_1,y_1)
er=np.linalg.norm(u[1:-1,1:-1]-kkk.T[1:-1,1:-1],ord=1)/(n-1)**2
err=abs(u[1:-1,1:-1]-kkk.T[1:-1,1:-1]).max()
print(err)
```





