---
title: "現代数理統計学 第1章 演習問題 問1 自作解答"
emoji: "👏"
type: "tech"
topics:
  - "統計学"
published: true
---


## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第1章演習問題の問1について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/)です．

## 解答

$$
\begin{aligned}
A \varDelta B
&= (A \backslash B) \cup (B \backslash A) \\
&= (A \cap B^c) \cup (B \cap A^c) \\
\end{aligned}
$$

$$
\begin{aligned}
A^c \varDelta B^c
&= (A^c \backslash B^c) \cup (B^c \backslash A^c) \\
&= (A^c \cap B) \cup (B^c \cap A) \\
&= (B \cap A^c) \cup (A \cap B^c) \\
&= (A \cap B^c) \cup (B \cap A^c) \\
\end{aligned}
$$

よって，$A \varDelta B = A^c \varDelta B^c$が成り立つ．

$$
\begin{aligned}
A \varDelta B
&= (A \backslash B) \cup (B \backslash A) \\
&= (A \cap B^c) \cup (B \cap A^c) \\
&= ((A \cap B^c) \cup (A \cap A^c)) \cup ((B \cap A^c) \cup (B \cap B^c)) \\
&= (A \cap (B^c \cup A^c)) \cup (B \cap (A^c \cup B^c)) \\
&= (A \cap (A^c \cup B^c)) \cup (B \cap (A^c \cup B^c)) \\
&= (A \cup B) \cap (A^c \cup B^c) \\
&= (A \cup B) \cap (A \cap B)^c \\
&= (A \cup B) \backslash (A \cap B) \\
\end{aligned}
$$

よって，$A \varDelta B = (A \cup B) \backslash (A \cap B)$が成り立つ．

以上より

$$
A \varDelta B
= A^c \varDelta B^c
= (A \cup B) \backslash (A \cap B)
$$

が成り立つ．

確率については，

$$
\begin{aligned}
P(A \varDelta B)
&= P((A \cup B) \backslash (A \cap B)) \\
&= P(A \cup B) - P(A \cap B) \\
&= P(A) + P(B) - P(A \cap B) - P(A \cap B) \\
&= P(A) + P(B) - 2P(A \cap B) \\
\end{aligned}
$$

となる．

## 参考文献

- [現代数理統計学の基礎 共立出版](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
