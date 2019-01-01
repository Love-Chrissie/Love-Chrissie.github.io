---
title: fusc function problem of Kata
categories: 计算机
tags:
  - 递归
  - Kata
abbrlink: 2611
date: 2018-09-23 20:28:11
---
This Kata is a continuation of [Part 1](http://www.codewars.com/kata/the-fusc-function-part-1). The `fusc` function is defined recursively as follows:

```
fusc(0) = 0
fusc(1) = 1
fusc(2n) = fusc(n)
fusc(2n + 1) = fusc(n) + fusc(n + 1)
```

Your job is to produce the code for the `fusc` function. In this kata, your function will be tested with large values of `n` (more than 1000 bits), so you should be concerned about stack overflow and timeouts.

**NOTE: In JavaScript and PHP, your function will be tested with n up to 52 bits. This will still require a non-naive solution. This will also overflow 32-bit operators, but it will be integer arithmetic.**

Hint: Define `F(n, a, b) = a * fusc(n) + b * fusc(n + 1)` and provide a recursive definition of `F` *without* referencing `fusc`.

上面是我之前做这题时候的描述，现在再看[这题](http://www.codewars.com/kata/the-fusc-function-part-1)，题目描述都不一样了。。之前直接递归可能是测试数太大了，直接超出最大递归深度。现在这题改了可以通过了，代码就不贴了。
但是之前谷歌搜了半天搜到了一个叫[Stern's Diatomic Series](http://mathworld.wolfram.com/SternsDiatomicSeries.html)的东西，很有意思，这个递推公式的通项可以写成如下形式：

$$ a_{0}=0,a_{1}=1,a_{n}=\sum_{k=0}^{n-1}\limits \binom{k}{n-k-1}(mod\,2). $$

---
