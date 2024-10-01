---
title: "現代数理統計学 第2章 演習問題 問4 自作解答"
emoji: "👋"
type: "tech"
topics: []
published: false
---

## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第2章演習問題の問4について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/xian-dai)です．

## 解答

### $E[(X-t)^2]$の最小値

$$
\begin{align*}
E[(X-t)^2] &= E[X^2 -2tX + t^2] \\
&= E[X^2] - E[2tX] + E[t^2] \\
&= E[X^2] - 2tE[X] + t^2
\end{align*}
$$

これを$t$の式と見ると，$t$に関する2次関数であり

$$
\begin{align*}
E[X^2] - 2tE[X] + t^2
&= t^2  - 2E[X] t + E[X^2] \\
&= t^2  - 2E[X] t + E[X]^2 - E[X]^2 + E[X^2] \\
&= (t - E[X])^2 - E[X]^2 + E[X^2]  \\
&= (t - E[X])^2 + E[X^2] - E[X]^2 \\
&= (t - E[X])^2 + V[X]
\end{align*}
$$

よって，$t=E[X]$のとき最小値を取ることがわかる．

### $E[|X-t|]$の最小値
