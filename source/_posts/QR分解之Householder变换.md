---
title: QR分解之Householder变换
categories: 数学
tags: 矩阵与数值分析
abbrlink: 29605
date: 2018-10-19 20:25:24
---

定义Householder矩阵如下：
$$\boldsymbol{H}(\boldsymbol{w})=\boldsymbol{I}-\frac{2}{\boldsymbol{w}^T \boldsymbol{w}} \boldsymbol{w} \boldsymbol{w}^T$$
显然该矩阵具有如下性质：

1. $\boldsymbol{H}^T=\boldsymbol{H}$，即$\boldsymbol{H}$为对称阵；
2. $\boldsymbol{H}^T\boldsymbol{H}=\boldsymbol{I}$，即$\boldsymbol{H}$为正交阵；
3. 如果$\boldsymbol{H}\boldsymbol{x}=\boldsymbol{y}$，则$\parallel \vec{y}\parallel_2=\parallel \vec{x}\parallel_2$；反之，对于任意两个向量$\boldsymbol{x},\boldsymbol{y}\in \mathbb{R}^n$，若$\parallel \vec{y}\parallel_2=\parallel \vec{x}\parallel_2$，且$\vec{x}\neq\vec{y}$，则必存在Householder矩阵$\boldsymbol{H}$，使得$\boldsymbol{y}=\boldsymbol{H}\boldsymbol{x}$；
4. 设$\vec{x}=(x_1,x_2,\cdots,x_n)^T\in \mathbb{R}^n$且$\vec{x}\neq\vec{0}$，取$\vec{w}=\vec{x}\pm\parallel \vec{x}\parallel_2 \vec{e}_1$，则$\boldsymbol{H}(\boldsymbol{w})\boldsymbol{x}=\boldsymbol{H}(\boldsymbol{x}\pm\parallel \boldsymbol{x}\parallel_2 \boldsymbol{e}_1)\vec{x}=\pm\parallel \vec{x}\parallel_2 \vec{e}_1=\pm\parallel \vec{x}\parallel_2 (1,0,\cdots,0)^T$.

证明：(1),(2)显然，证明(3)显然有：
$$\parallel \boldsymbol{y}\parallel_2^2=\boldsymbol{y}^T\boldsymbol{y}=(\boldsymbol{H}\boldsymbol{x})^T(\boldsymbol{H}\boldsymbol{x})=\boldsymbol{x}^T(\boldsymbol{H}^T\boldsymbol{H})\boldsymbol{x}=\boldsymbol{x}^T\boldsymbol{x}=\parallel\boldsymbol{x}\parallel_2^2$$
反之，若$\parallel \vec{y}\parallel_2=\parallel \vec{x}\parallel_2$，且$\vec{x}\neq\vec{y}$,令$\boldsymbol{w}=\boldsymbol{x}-\boldsymbol{y}$,有：
$$\parallel\boldsymbol{w}\parallel_2^2=(\boldsymbol{x}-\boldsymbol{y})^T(\boldsymbol{x}-\boldsymbol{y})=(2\boldsymbol{x}-(\boldsymbol{x}+\boldsymbol{y}))^T(\boldsymbol{x}-\boldsymbol{y})=2\boldsymbol{x}^T(\boldsymbol{x}-\boldsymbol{y})$$

$$\begin{align}\boldsymbol{H}(\boldsymbol{w})\boldsymbol{x}&=(\boldsymbol{I}-\frac{2}{\boldsymbol{w}^T \boldsymbol{w}} \boldsymbol{w} \boldsymbol{w}^T)\boldsymbol{x}=(\boldsymbol{I}-\frac{2}{\parallel\boldsymbol{x}-\boldsymbol{y}\parallel_2^2} (\boldsymbol{x}-\boldsymbol{y}) (\boldsymbol{x}-\boldsymbol{y})^T)\boldsymbol{x}\\\\
&=\boldsymbol{x}-\frac{2(\boldsymbol{x}-\boldsymbol{y})^T\boldsymbol{x}}{\parallel\boldsymbol{x}-\boldsymbol{y}\parallel_2^2}(\boldsymbol{x}-\boldsymbol{y})=\boldsymbol{x}-(\boldsymbol{x}-\boldsymbol{y})=\boldsymbol{y}\end{align}$$

性质(4)由性质(3)自然得出。

$m\times n$阶矩阵三角化过程
记
$$
A_{m\times n}^{(1)}=A_{m\times n}=\begin{bmatrix}a_{11}^{(1)} & a_{12}^{(1)} & \cdots & a_{1n}^{(1)}\\\\a_{21}^{(1)} & a_{22}^{(1)} & \cdots & a_{2n}^{(1)}\\\\
\vdots & \vdots & \ddots & \vdots\\\\a_{m1}^{(1)} & a_{m2}^{(1)} & \cdots & a_{mn}^{(1)}\end{bmatrix}$$

取正交矩阵$Q_1=H_1$(依性质4取Householder矩阵)，这里$H_1$是将$m$维向量$(a_{11}^{(1)}, a_{21}^{(1)},\cdots,a_{m1}^{(1)})^T$变换为$m$维向量$(k_1, 0,\cdots,0)^T$的Householder变换矩阵

$$H_1=I_m-\alpha_1 \boldsymbol{u}_1 \boldsymbol{u}_1^T$$
这里
$$|k_1|^2=\boldsymbol{x}^T \boldsymbol{x},\boldsymbol{u}=\boldsymbol{x-k_1\boldsymbol{e}_1},\alpha=\frac{1}{k_1(k_1-\boldsymbol{e}_1^T \boldsymbol{x})}=\frac{2}{\boldsymbol{u}^T\boldsymbol{u}}$$

得到
$$A_{m\times n}^{(2)}=Q_1 A_{m\times n}^{(1)}=\begin{bmatrix}k_1 & a_{12}^{(2)} & \cdots & a_{1n}^{(2)}\\\\0 & a_{22}^{(2)} & \cdots & a_{2n}^{(2)}\\\\
\vdots & \vdots & \ddots & \vdots\\\\0 & a_{m2}^{(2)} & \cdots & a_{mn}^{(2)}\end{bmatrix}$$

这里
$$
\begin{bmatrix}a_{1,j}^{(2)}\\\\a_{2,j}^{(2)}\\\\ \vdots \\\\ a_{m,j}^{(2)}\end{bmatrix}=H_1\begin{bmatrix}a_{1,j}^{(1)}\\\\a_{2,j}^{(1)}\\\\ \vdots \\\\ a_{mj}^{(1)}\end{bmatrix}=\begin{bmatrix}a_{1,j}^{(1)}\\\\a_{2,j}^{(1)}\\\\ \vdots \\\\ a_{mj}^{(1)}\end{bmatrix}-\alpha_1\sum\limits_{l=1}^{m}u_{1l}a_{l,j}^{(1)}\boldsymbol{u}_1\quad\,j=2,3,\cdots,n$$

一般第$k$步取正交矩阵$Q_k$
$$Q_k=\begin{bmatrix}I_{k-1} & \quad \\\\ \quad & H_k\end{bmatrix}$$
这里$H_k$是将$m-k+1$维向量$(a_{k,k}^{(k)},a_{k+1,k}^{(k)},\cdots,a_{m,k}^{(k)})^T$变换为$m-k+1$维向量$(k_k,0,\cdots,0)^T$的Householder矩阵

$$H_k=I_{m-k+1}-\alpha_k \boldsymbol{u}_k \boldsymbol{u}_k^T$$

这里$\boldsymbol{u}_k$为$m-k+1$维向量，这时

$$A_{m\times n}^{(k+1)}=Q_1 A_{m\times n}^{(k)}=\begin{bmatrix}k_1 & a_{1,2}^{(2)} & \cdots & a_{1,k}^{(2)} & a_{1,k+1}^{(2)} & \cdots & a_{1,n}^{(2)}\\\\  & k_2 & \cdots & a_{2,k}^{(3)} & a_{2,k+1}^{(3)} & \cdots & a_{2,n}^{(3)}\\\\
 &  & \ddots & \cdots & \cdots & \cdots & \cdots\\\\  &   &   & k_k & a_{k,k+1}^{(k+1)} & \cdots & a_{k,n}^{(k+1)}\\\\& & & & a_{k+1,k+1}^{(k+1)} & \cdots & a_{k+1,n}^{(k+1)}\\\\& & & & \cdots & \cdots & \cdots\\\\& & & & a_{m,k+1}^{(k+1)} & \cdots & a_{m,n}^{(k+1)} \end{bmatrix}$$

其中
$$
\begin{bmatrix}a_{k,j}^{(k+1)}\\\\a_{k+1,j}^{(k+1)}\\\\ \vdots \\\\ a_{m,j}^{(k+1)}\end{bmatrix}=H_k\begin{bmatrix}a_{k,j}^{(k)}\\\\a_{k+1,j}^{(k)}\\\\ \vdots \\\\ a_{mj}^{(k)}\end{bmatrix}=\begin{bmatrix}a_{k,j}^{(k)}\\\\a_{k+1,j}^{(k)}\\\\ \vdots \\\\ a_{mj}^{(k)}\end{bmatrix}-\alpha_k\sum\limits_{l=1}^{m-k+1}u_{kl}a_{k+l-1,j}^{(k)}\boldsymbol{u}_k\quad\,j=k+1,\cdots,n,\text{其他元素不变}$$

记$s=\min(m-1,n)$则当$k=s$时即可完成矩阵的三角化过程，即
$$QA=Q_s Q_{s-1} \cdots Q_1 A=R$$
由于$Q$为正交矩阵，所以
$$A=Q^T R$$

$QR$分解的python代码如下

```python
import numpy as np
def householder(A, y):
    row = np.shape(A)[0]
    col = np.shape(A)[1]
    u = np.zeros(row)
    for i in range(col):
        # 计算第i列模
        aa = 0.0
        for l in range(i, row):
            aa += A[l, i]*A[l, i]
        aa = np.sqrt(aa)

        # 防止分母过小
        if A[i, i] > 0.0 :
            ki = -aa
        else:
            ki = aa
        alpha = 1.0/(ki*(ki-A[i, i]))
        u[i] = A[i, i] - ki
        A[i, i] = ki
        for l in range(i+1, row):
            u[l] = A[l, i]
            A[l, i] = 0.0
        for j in range(i+1, col):
            aa = 0.0
            for l in range(i, row):
                aa += u[l] * A[l, j]
            aa = alpha * aa
            for l in range(i, row):
                A[l, j] -= aa * u[l]
        aa = 0.0
        for l in range(i, row):
            aa += u[l] * y[l]
        aa *= alpha
        for l in range(i, row):
            y[l] -= aa * u[l]
    print("Matrix HA, and Hy:")
    for i in range(row):
        for j in range(col):
            print("{:14.8f}".format(A[i, j]), end='')
        print("  |{:14.8f}".format(y[i]))
```


---
