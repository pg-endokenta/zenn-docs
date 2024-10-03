---
title: "現代数理統計学の基礎 第3章 演習問題 問3 自作解答"
emoji: "⛳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学"]
published: true
---


## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第3章演習問題の問3について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/)です．

## 解答

### 確率が1となることの証明

$\sum_{x=0}^{K} P(X=x|N,M,K) = 1$が成り立つことを示す．

$$
P(X=x|N,M,K) = \frac{\binom{M}{x} \binom{N-M}{K-x}}{\binom{N}{K}}, \quad x=0,1,\ldots,K
$$

より，

$$
\begin{align}
\sum_{x=0}^{K} P(X=x|N,M,K) = \sum_{x=0}^{K} \frac{\binom{M}{x} \binom{N-M}{K-x}}{\binom{N}{K}}
\end{align}
$$

である．$\sum_{x=0}^{K} P(X=x|N,M,K)$が$1$となることは，
$(1)$の右辺において$(分母)=(分子)$となることと同値であり，

$$
\begin{align}
    \binom{N}{K} &= \sum_{x=0}^{K} \binom{M}{x} \binom{N-M}{K-x}
\end{align}
$$

を示せば良い．
これを示すために
$(a+b)^N = (a+b)^M (a+b)^{N-M}$の2項展開を考える．
それぞれを2項展開すると

$$
\begin{align}
\sum_{K=0}^{N} \binom{N}{K} a^{K} b^{N-K}
&= \sum_{x=0}^{M} \binom{M}{x} a^{x} b^{M-x} \sum_{y=0}^{N-M} \binom{N-M}{y} a^{y} b^{N-M-y}
\end{align}
$$

となる．これは恒等式であるから，左辺と右辺の$a^Kb^{N-K}$の係数は等しくなる．
よって，

$$
\begin{align}
\binom{N}{K}
&= \sum_{\substack{
x \in \mathbb{Z} \\
x + y = K \\
0 \leq x \leq K \\
}} \binom{M}{x} \binom{N-M}{y}
&= \sum_{x=0}^{K} \binom{M}{x} \binom{N-M}{K-x}
\end{align}
$$

が成り立つことがわかる．
以上より，
$\sum_{x=0}^{K} P(X=x|N,M,K) = 1$が成り立つことが示された．

### 期待値の計算

$$
\begin{align}
E[X]
&= \sum_{x=0}^{K} x P(X=x|N,M,K) \\
&= \sum_{x=0}^{K} x \frac{\binom{M}{x} \binom{N-M}{K-x}}{\binom{N}{K}} \\
&= \sum_{x=1}^{K} x \frac{\binom{M}{x} \binom{N-M}{K-x}}{\binom{N}{K}} \\
&= \frac{1}{\binom{N}{K}}\sum_{x=1}^{K} x \binom{M}{x} \binom{N-M}{K-x} \\
&= \frac{1}{\binom{N}{K}}\sum_{x=1}^{K} x \frac{M!}{x! (M-x)!}\binom{N-M}{K-x} \\
&= \frac{1}{\binom{N}{K}}\sum_{x=1}^{K}\frac{M!}{(x-1)! (M-x)!}\binom{N-M}{K-x} \\
&= \frac{1}{\binom{N}{K}}\sum_{x=1}^{K} M \frac{(M-1)!}{(x-1)! (M-x)!}\binom{N-M}{K-x} \\
&= \frac{1}{\binom{N}{K}}\sum_{x=1}^{K} M\binom{M-1}{x-1}\binom{N-M}{K-x} \\
&= \frac{M}{\binom{N}{K}}\sum_{x=1}^{K}\binom{M-1}{x-1}\binom{N-M}{K-x} \\
&= \frac{M}{\binom{N}{K}}\sum_{x'=0}^{K-1}\binom{M-1}{x'}\binom{N-M}{K-x'-1} \\
&= \frac{M}{\binom{N}{K}}\sum_{x'=0}^{K-1}\binom{M-1}{x'}\binom{(N-1)-(M-1)}{(K-1)-x'} \\
&= \frac{M}{\binom{N}{K}}\binom{N-1}{K-1} \\
&= M \times \frac{K!(N-K)!}{N!} \times \frac{(N-1)!}{(K-1)!(N-K)!} \\
&= M \times \frac{K}{N} \\
&= K \frac{M}{N}
\end{align}
$$

### 分散の計算

はじめに$E[X(X-1)]$を計算する．

$$
\begin{align}
E[X(X-1)]
&= \sum_{x=0}^{K} x(x-1) P(X=x|N,M,K) \\
&= \sum_{x=0}^{K} x(x-1) \frac{\binom{M}{x} \binom{N-M}{K-x}}{\binom{N}{K}} \\
&= \sum_{x=2}^{K} x(x-1) \frac{\binom{M}{x} \binom{N-M}{K-x}}{\binom{N}{K}} \\
&= \frac{1}{\binom{N}{K}}\sum_{x=2}^{K} x(x-1) \binom{M}{x} \binom{N-M}{K-x} \\
&= \frac{1}{\binom{N}{K}}\sum_{x=2}^{K} x(x-1) \frac{M!}{x! (M-x)!}\binom{N-M}{K-x} \\
&= \frac{1}{\binom{N}{K}}\sum_{x=2}^{K}\frac{M!}{(x-2)! (M-x)!}\binom{N-M}{K-x} \\
&= \frac{1}{\binom{N}{K}}\sum_{x=2}^{K} M(M-1) \frac{(M-2)!}{(x-2)! (M-x)!}\binom{N-M}{K-x} \\
&= \frac{1}{\binom{N}{K}}\sum_{x=2}^{K} M(M-1)\binom{M-2}{x-2}\binom{N-M}{K-x} \\
&= \frac{M(M-1)}{\binom{N}{K}}\sum_{x=2}^{K}\binom{M-2}{x-2}\binom{N-M}{K-x} \\
&= \frac{M(M-1)}{\binom{N}{K}}\sum_{x'=0}^{K-2}\binom{M-2}{x'}\binom{N-M}{K-x'-2} \\
&= \frac{M(M-1)}{\binom{N}{K}}\sum_{x'=0}^{K-2}\binom{M-2}{x'}\binom{(N-2)-(M-2)}{(K-2)-x'} \\
&= \frac{M(M-1)}{\binom{N}{K}}\binom{N-2}{K-2} \\
&= M(M-1) \times \frac{K!(N-K)!}{N!} \times \frac{(N-2)!}{(K-2)!(N-K!)} \\
&= M(M-1) \times \frac{K(K-1)}{N(N-1)} \\
&= K(K-1) \frac{M(M-1)}{N(N-1)}
\end{align}
$$

よって

$$
\begin{align}
V[X]
&= E[X(X-1)] + E[X] - E[X]^2 \\
&= K(K-1) \frac{M(M-1)}{N(N-1)} + K \frac{M}{N} - \left(K \frac{M}{N}\right)^2 \\
&= \frac{1}{N^2(N-1)}
\left(
K(K-1)M(M-1)N + KMN(N-1) - K^2M^2(N-1)
\right) \\
&= \frac{KM}{N^2(N-1)}
\left(
(K-1)(M-1)N + N(N-1) - KM(N-1)
\right) \\
&= \frac{KM}{N^2(N-1)}
\left(
KMN -KN -MN + N + N(N-1) - KMN +KM
\right) \\
&= \frac{KM}{N^2(N-1)}
\left( -KN -MN + N + N(N-1) + KM
\right) \\
&= \frac{KM}{N^2(N-1)}
\left( -KN -MN + N^2 + KM
\right) \\
&= \frac{KM}{N^2(N-1)}
\left(N^2 - (K+M)N + KM
\right) \\
&= \frac{KM(N-K)(N-M)}{N^2(N-1)} \\
&= \frac{N-K}{N-1}K\frac{M}{N}\frac{N-M}{N} \\
&= \frac{N-K}{N-1}K\frac{M}{N}\left(1-\frac{M}{N}\right)
\end{align}
$$

となる．

## 参考文献

- [久保川 達也．現代数理統計学の基礎．共立出版．](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
- [稲垣宣生．数理統計学（改訂版）．裳華房．](https://www.shokabo.co.jp/mybooks/ISBN978-4-7853-1411-8.htm)
