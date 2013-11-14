---
layout: modern
title: 如何把贝叶斯定理推倒（在床上）
---

我们都知道条件概率是什么——

<img src="http://chart.googleapis.com/chart?cht=tx&chl=P(A%7CB)%3D%5Cfrac%7BP(A%5Ccap%20B)%7D%7BP(B)%7D" style="border:none;" />

然后把左边的A B掉换位置...

<img src="http://chart.googleapis.com/chart?cht=tx&chl=P(B%7CA)%3D%5Cfrac%7BP(A%5Ccap%20B)%7D%7BP(A)%7D" style="border:none;" />

所以——

<img src="http://chart.googleapis.com/chart?cht=tx&chl=P(A%5Ccap%20B)%3DP(A)P(B%7CA)" style="border:none;" />

接着所以——

<img src="http://chart.googleapis.com/chart?cht=tx&chl=P(A%7CB)%3D%5Cfrac%7BP(B%7CA)P(A)%7D%7BP(B)%7D" style="border:none;" />

然后我们就得到了贝叶斯定理（Bayes' Theorem），个人认为它的作用是能使人们根据新的信息去修改自己的已有观点。

外部链接：<a href="http://en.wikipedia.org/wiki/Bayes%27_theorem">贝叶斯定理在维基百科</a>