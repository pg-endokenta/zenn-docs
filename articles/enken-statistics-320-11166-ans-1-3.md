---
title: "現代数理統計学の基礎 第1章 演習問題 問3 自作解答"
emoji: "💎"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学"]
published: true
---


## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第1章演習問題の問3について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/)です．

## 解答

条件付き確率の定義より

$$
\begin{aligned}
P(A|B) &= \frac{P(A \cap B)}{P(B)} \\
P(A \cap B) &= P(A|B)P(B) \\
\end{aligned}
$$

が成り立つ．

これは$k$を用いて

$$
\begin{aligned}
P(A_1 \cap \cdots A_{k-1} \cap A_k)
&= P(A_k|A_1 \cap \cdots \cap A_{k-1})P(A_1 \cap \cdots \cap A_{k-1}) \\
\end{aligned}
$$

と書くことができる．

この$k$を$n$から$2$まで$1$ずつ変化させながら適用すると，

$$
\begin{aligned}
P(A_1 \cap \cdots \cap A_n)
&= P(A_n|A_1 \cap \cdots \cap A_{n-1})P(A_1 \cap \cdots \cap A_{n-1}) \\
&= P(A_n|A_1 \cap \cdots \cap A_{n-1})P(A_{n-1}|A_1 \cap \cdots \cap A_{n-2})P(A_1 \cap \cdots \cap A_{n-2}) \\
&= \cdots \\
&= P(A_n|A_1 \cap \cdots \cap A_{n-1})P(A_{n-1}|A_1 \cap \cdots \cap A_{n-2}) \cdots P(A_2|A_1)P(A_1) \\
\end{aligned}
$$

となることが分かる．

## 参考文献

- [久保川 達也．現代数理統計学の基礎．共立出版．](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
