---
title: "現代数理統計学の基礎 第1章 演習問題 問2 自作解答"
emoji: "🦝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学"]
published: true
---


## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第1章演習問題の問2について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/)です．

## 解答

左辺を式変形し右辺を導くことで示す．

$$
\begin{aligned}
P(A_1 \cup A_2 \cup A_3)
&= P(A_1) + P(A_2 \cup A_3) - P(A_1 \cap (A_2 \cup A_3)) \\
&= P(A_1) + P(A_2) + P(A_3) - P(A_2 \cap A_3) -  P(A_1 \cap (A_2 \cup A_3)) \\
&= P(A_1) + P(A_2) + P(A_3) - P(A_2 \cap A_3) -  P((A_1 \cap A_2) \cup (A_1 \cap A_3)) \\
&= P(A_1) + P(A_2) + P(A_3) - P(A_2 \cap A_3) - ( P(A_1 \cap A_2) + P(A_1 \cap A_3) - P((A_1 \cap A_2) \cap (A_1 \cap A_3))) \\
&= P(A_1) + P(A_2) + P(A_3) - P(A_2 \cap A_3) - P(A_1 \cap A_2) - P(A_1 \cap A_3) + P(A_1 \cap A_2 \cap A_3) \\
&= P(A_1) + P(A_2) + P(A_3) - P(A_1 \cap A_2) - P(A_2 \cap A_3) - P(A_3 \cap A_1) + P(A_1 \cap A_2 \cap A_3) \\
\end{aligned}
$$

よって示された．

## 参考文献

- [久保川 達也．現代数理統計学の基礎．共立出版．](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
