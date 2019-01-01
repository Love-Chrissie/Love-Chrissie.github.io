---
title: 正定矩阵的cholesky分解
abbrlink: 56208
date: 2018-10-12 10:27:00
categories: 数学
tags: 矩阵与数值分析
---

### 正定矩阵的cholesky分解
由于正定矩阵的主子式均大于零，可得正定矩阵的顺序主子式均大于零，所以正定矩阵$\boldsymbol A$有唯一的$\boldsymbol{LDU}$分解，即：
$$
\boldsymbol A = \boldsymbol{LDU}$$
这里$\boldsymbol L$为单位下三角矩阵，$\boldsymbol U$为单位上三角矩阵，$\boldsymbol D$为对角矩阵。又$\boldsymbol A$是对称矩阵，故：
$$
\boldsymbol A = \boldsymbol A^T=(\boldsymbol{LDU})^T=\boldsymbol U^T \boldsymbol D \boldsymbol L^T$$

根据$\boldsymbol{LDU}$分解的唯一性得
$$
\boldsymbol U=\boldsymbol L^T$$
故正定矩阵$\boldsymbol A$有分解式
$$\boldsymbol A = \boldsymbol L \boldsymbol D \boldsymbol L^T$$
这里$\boldsymbol L$的对角元素皆为1.记
$$\boldsymbol D = diag(d_1,d_2,\cdots,d_n)$$
由$\boldsymbol A$的正定性可得
$$d_i>0,i=1,2,\cdots,n$$
若记
$$D^{\frac{1}{2}}=diag(\sqrt{d_1},\sqrt{d_2},\cdots,\sqrt{d_n})$$
则
$$\boldsymbol A = \boldsymbol L\boldsymbol D^{\frac{1}{2}}\boldsymbol D^{\frac{1}{2}}\boldsymbol L^T=(\boldsymbol L\boldsymbol D^{\frac{1}{2}})(\boldsymbol L\boldsymbol D^{\frac{1}{2}})^T=\widetilde{\boldsymbol L} \widetilde{\boldsymbol L}^T$$
这里$\widetilde{\boldsymbol L}=\boldsymbol L \boldsymbol D^{\frac{1}{2}}$是下三角矩阵，其对角元素皆为正数，则这种分解也是唯一的。称之为正定矩阵的Cholesky分解。
#### 计算公式
由
$$\boldsymbol A = \begin{pmatrix}a_{11} & a_{12} & \cdots & a_{1n}\\\\
a_{21} & a_{22} & \cdots & a_{2n}\\\\\
\vdots & \vdots & \ddots & \vdots\\\\\
a_{n1} & a_{n2} & \cdots & a_{nn}\end{pmatrix}=\begin{pmatrix}l_{11} &  &  & \\\\
l_{21} & l_{22} &  & \\\\\
\vdots & \vdots & \ddots & \\\\\
l_{n1} & l_{n2} & \cdots & l_{nn}\end{pmatrix}\begin{pmatrix}l_{11} & l_{21} & \cdots & l_{n1}\\\\
 & l_{22} & \cdots & l_{n2}\\\\\
 &  & \ddots & \vdots \\\\\
 &  &  & l_{nn}\end{pmatrix}=\boldsymbol L \boldsymbol L^T$$

 矩阵对应每项相等可以得到矩阵$\boldsymbol L$的各项计算公式：
 $$
 a_{ik}=\sum\limits_{s=1}^{k-1}l_{is}l_{ks}+l_{kk}^2$$
 所以：
 $$l_{kk}=\sqrt{a_{kk}-\sum\limits_{s=1}^{k-1}l_{ks}^2}\\\\
 l_{ik}=\frac{a_{ik}-\sum\limits_{s=1}^{k-1}l_{is}l_{ks}}{l_{kk}},\quad i=k+1,\cdots,n$$

python代码如下：

```python
def chollt(A):
    EPSILON = 1e-8
    DIM = len(A)
    for k in range(DIM):
        for i in range(k, DIM):
            for j in range(k):
                A[i, k] = A[i, k] - A[i, j] * A[k, j]
        if np.fabs(A[k, k]) < EPSILON:
            return 1
        A[k, k] = np.math.sqrt(A[k, k])
        for i in range(k+1, DIM):
            A[i, k] = A[i, k] / A[k, k]
    return 0
```

---
