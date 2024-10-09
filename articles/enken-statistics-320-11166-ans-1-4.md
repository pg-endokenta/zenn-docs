---
title: "現代数理統計学の基礎 第1章 演習問題 問4 自作解答"
emoji: "🦬"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学"]
published: true
---


## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第1章演習問題の問4について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/)です．

## 解答

### (1)

１回サイコロを投げることを考え，$A$, $B$の事象を次のように考える．
※ $A, B$のために計2回投げるわけではない．

$$
\begin{aligned}
A &= \{1\} \\
B &= \{1, 2\}
\end{aligned}
$$

このとき

$$
\begin{aligned}
(左辺)
&= P(A|B^c) \\
&= \frac{P(A \cap B^c)}{P(B^c)} \\
&= \frac{P(\{\})}{P(\{3,4,5,6\})} \\
&= 0
\end{aligned}
$$

$$
\begin{aligned}
(右辺)
&= 1 - P(A|B) \\
&= 1 - \frac{P(A \cap B)}{P(B)} \\
&= 1 - \frac{P(\{1\})}{P(\{1,2\})} \\
&= 1 - \frac{\frac{1}{6}}{\frac{2}{6}} \\
&= 1 - \frac{1}{2} \\
&= \frac{1}{2}
\end{aligned}
$$

よって成り立たない例であることがわかる．

### (2)

１回サイコロを投げることを考え，$A$, $B$, $C$の事象を次のように考える．
※ $A, B, C$のために計3回投げるわけではない．

$$
\begin{aligned}
A &= \{1\} \\
B &= \{1\} \\
C &= \{1, 2\}
\end{aligned}
$$

このとき

$$
\begin{aligned}
(左辺)
&= P(C|A \cup B) \\
&= \frac{P(C \cap (A \cup B))}{P(A \cup B)} \\
&= \frac{P(\{1\})}{P(\{1\})} \\
&= 1
\end{aligned}
$$

$$
\begin{aligned}
(右辺)
&= P(C|A) + P(C|B) \\
&= \frac{P(C \cap A)}{P(A)} + \frac{P(C \cap B)}{P(B)} \\
&= \frac{P(\{1\})}{P(\{1\})} + \frac{P(\{1\})}{P(\{1\})} \\
&= 1 + 1 \\
&= 2
\end{aligned}
$$

よって成り立たない例であることがわかる．

## 参考文献

- [久保川 達也．現代数理統計学の基礎．共立出版．](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
