---
title: "現代数理統計学の基礎 第3章 演習問題 問5 自作解答"
emoji: "⛳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学"]
published: true
---


## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第3章演習問題の問5について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/)です．

## 解答

$$
\lambda(t) = \frac{f(t)}{1-F(t)}
$$

の両辺を積分すると，

$$
\begin{aligned}
\int_0^x \lambda(t) dx &= \int_0^x \frac{f(t)}{1-F(t)} dx \\
\int_0^x \lambda(t) dx &= -\int_0^x -\frac{f(t)}{1-F(t)} dx \\
\int_0^x \lambda(t) dx &= -\int_0^x \frac{(1-F(t))'}{1-F(t)} dx \\
\int_0^x \lambda(t) dx &= -[\log(1-F(t))]_0^x \\
\int_0^x \lambda(t) dx &= -\log(1-F(x)) \\
-\int_0^x \lambda(t) dx &= \log(1-F(x)) \\
\exp(-\int_0^x \lambda(t) dx) &= 1-F(x) \\
F(x) &= 1-\exp(-\int_0^x \lambda(t) dx)
\end{aligned}
$$

となる．
これを$x$について微分すると，

$$
\begin{aligned}
f(x) &= \frac{d}{dx} \left[ 1-\exp(-\int_0^x \lambda(t) dt) \right] \\
&= 0 - \frac{d}{dx} \exp(-\int_0^x \lambda(t) dt) \\
&= \exp(-\int_0^x \lambda(t) dt) \frac{d}{dx} \int_0^x \lambda(t) dt \\
&= \exp(-\int_0^x \lambda(t) dt) \lambda(x) \\
&= \lambda(x) \exp(-\int_0^x \lambda(t) dt)
\end{aligned}
$$

となる．

## 参考文献

- [久保川 達也．現代数理統計学の基礎．共立出版．](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
