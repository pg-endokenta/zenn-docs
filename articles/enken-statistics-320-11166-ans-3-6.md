---
title: "現代数理統計学の基礎 第3章 演習問題 問6 自作解答"
emoji: "⛳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学"]
published: true
---


## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第3章演習問題の問6について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/)です．

## 解答

$$
\begin{aligned}
P(Y = y)
&= P([X] = y) \\
&= P(y \leq X < y+1) \\
&= P(X < y+1) - P(X < y) \\
&= F_X(y+1) - F_X(y) \\
&= (1 - e^{-\lambda(y+1)}) - (1 - e^{-\lambda y}) \\
&= e^{-\lambda y} - e^{-\lambda(y+1)} \\
&= e^{-\lambda y} - e^{-\lambda y}e^{-\lambda} \\
&= e^{-\lambda y}(1 - e^{-\lambda}) \\
\end{aligned}
$$
ここで，$p=1-e^{-\lambda}$とおくと，

$$
P(Y = y) = (1-p)^y p
$$

であり，これは幾何分布の確率関数である．
よって，$Y$は幾何分布に従う．

幾何分布は無記憶性をもつため

$$
P[Y \geq t+s | Y \geq s] = P[Y \geq s]
$$

が成り立つ．

## 参考文献

- [久保川 達也．現代数理統計学の基礎．共立出版．](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
