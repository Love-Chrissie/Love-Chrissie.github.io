---
title: Fibonacci序列
categories: 计算机
tags: 算法
abbrlink: 5621
date: 2018-10-10 14:19:21
---

### 从Fibonacci序列谈起
#### 定义

$F_0=0,\quad F_1=1,\quad F_n=F_{n-1}+F_{n-2}\quad (n>1)$

递归算法的$F_n$计算时间复杂度为$O(2^n)$，为指数时间。空间复杂度为$S_n=O(n)$为线性空间。

改用备忘录的方式计算Fibonacci序列可以更节约时间。类似如下方式：

| $F_0$ | $F_1$ | $F_2$ | $F_3$ | $F_4$ | $F_5$ |
|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
|   0   | 1     | 1     | 2     | 3     | 5     |

但空间仍然是$O(n)$，如果只需要求$F_n$则有很大空间浪费。所以我们只需要保存前两项即可。
$P_1=0,P_2=1,C=P_1+P_2=1$,下一次赋值结果为$P_1=1,P_2=1,C=2$,时间复杂度为$O(n)$,空间复杂度为$O(1)$。

更好的方式：
使用Fibonacci序列的矩阵形式
$$\begin{align}\begin{pmatrix}
F_{n+1}\\\\
F_n
\end{pmatrix}&=\begin{pmatrix}
1 & 1\\\\
1 & 0
\end{pmatrix}
\begin{pmatrix}
F_{n}\\\\
F_{n-1}
\end{pmatrix}\\\\&=\begin{pmatrix}
1 & 1\\\\
1 & 0
\end{pmatrix}^2
\begin{pmatrix}
F_{n-1}\\\\
F_{n-2}
\end{pmatrix}\\\\&\cdots\\\\
&=\begin{pmatrix}
1 & 1\\\\
1 & 0
\end{pmatrix}^n
\begin{pmatrix}
F_{1}\\\\
F_{0}
\end{pmatrix}
\end{align}
$$

即最后结果为：
$$\begin{pmatrix}
F_{n+1}\\\\
F_n
\end{pmatrix}=\begin{pmatrix}
1 & 1\\\\
1 & 0
\end{pmatrix}^n
\begin{pmatrix}
F_{1}\\\\
F_{0}
\end{pmatrix}
$$

下面用一个简单方法处理计算$\begin{pmatrix}1 & 1\\\\1 & 0\end{pmatrix}^n$


$\text{令：}A=\begin{pmatrix}
1 & 1\\\\
1 & 0
\end{pmatrix},\text{那么}A^n=\begin{pmatrix}
F_{n+1} & F_n\\\\
F_n & F_{n-1}
\end{pmatrix}\text{归纳易证}$

$\text{所以}A^{2m}=\begin{pmatrix}
F_{2m+1} & F_{2m}\\\\
F_{2m} & F_{2m-1}
\end{pmatrix}=A^m\cdot A^m,\quad A^m=\begin{pmatrix}
F_{m+1} & F_m\\\\
F_m & F_{m-1}
\end{pmatrix}\\\\
\begin{align}
so:\begin{pmatrix}
F_{2m+1} & F_{2m}\\\\
F_{2m} & F_{2m-1}
\end{pmatrix}&=
\begin{pmatrix}
F_{m+1} & F_m\\\\
F_m & F_{m-1}
\end{pmatrix}
\begin{pmatrix}
F_{m+1} & F_m\\\\
F_m & F_{m-1}
\end{pmatrix}\\\\
&=\begin{pmatrix}
F_{m+1}^2+F_m^2 & F_{m+1}F_m+F_m F_{m-1}\\\\
F_{m+1}F_m+F_m F_{m-1} & F_{m}^2+F_{m-1}^2
\end{pmatrix}  \end{align}$

$\Longrightarrow \begin{cases}
F_{2m+1}=F_{m+1}^2+F_m^2\\\\F_{2m}=F_m(F_{m+1}+ F_{m-1})
\end{cases}\text{得到了Fibonacci序列的另一种递推公式}$

1. $n$为奇数，即$n=2m+1，\lfloor\frac{n}{2}\rfloor=m$
$$\begin{pmatrix}
F_{n+1}\\\\
F_{n}
\end{pmatrix}=\begin{pmatrix}
F_{2m+2}\\\\
F_{2m+1}
\end{pmatrix}=\begin{pmatrix}
(2F_{m}+F_{m+1})F_{m+1}\\\\
F_{m}^2+F_{m+1}^2
\end{pmatrix}$$
2. n为偶数，即$n=2m，\lfloor\frac{n}{2}\rfloor=m$
$$\begin{pmatrix}
F_{n+1}\\\\
F_{n}
\end{pmatrix}=\begin{pmatrix}
F_{2m+1}\\\\
F_{2m}
\end{pmatrix}=\begin{pmatrix}
F_{m}^2+F_{m+1}^2\\\\
(2F_{m+1}-F_{m})F_{m}
\end{pmatrix}$$

> 这里仅用第m项与第m+1项表达，计算过程中的m-1项和m+2项利用Fibonacci数列的递推公式代换掉了。

所以对于$Fibonacci(n)$我们只需要计算$Fibonacci(n/2)=Fibonacci(m)$。其时间复杂度为$O(\log n)$，空间复杂度也为$O(\log n)$。

python代码如下：
```python
def Fibonacci(n):
    if n<=0:
        return (0, 1)
    f_m, f_m1 = Fibonacci(n/2)
    if n%2:
        return f_m**2+f_m1**2, (2*f_m+f_m1)*f_m1
    return (2*f_m1-f_m)*f_m1, f_m**2+f_m1**2
```


---
