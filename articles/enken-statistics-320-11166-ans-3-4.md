---
title: "現代数理統計学の基礎 第3章 演習問題 問4 自作解答"
emoji: "⛳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学"]
published: true
---


## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第3章演習問題の問4について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/)です．

## 解答

$$
\begin{align}
\lim_{n\to \infty} P(X=x|N,M,K)
&= \lim_{n\to \infty} \frac{\binom{M}{x} \binom{N-M}{K-x}}{\binom{N}{K}} \\
&= \lim_{n\to \infty} \frac{M!}{x! (M-x)!}\frac{(N-M)!}{(K-x)!(N-M-K+x)!} \frac{K!(N-K)!}{N!} \\
&= \lim_{n\to \infty} \frac{K!}{x!(K-x)!} \frac{M!}{(M-x)!} \frac{(N-M)!}{(N-M-K+x)!} \frac{(N-K)!}{N!} \\
&= \lim_{n\to \infty} \binom{K}{x} \frac{M!}{(M-x)!} \frac{(N-M)!}{(N-M-K+x)!} \frac{(N-K)!}{N!} \\
&= \lim_{n\to \infty} \binom{K}{x} \frac{M(M-1)\cdots(M-(x-1))}{1} \frac{(N-M)!}{(N-M-(K-x))!} \frac{1}{N(N-1)\cdots(N-(K-1))} \\
&= \lim_{n\to \infty} \binom{K}{x} \frac{M(M-1)\cdots(M-(x-1))}{1} \frac{(N-M)(N-M-1)\cdots(N-M-(K-x-1))}{1} \frac{1}{N(N-1)\cdots(N-(K-1))} \\
&= \lim_{n\to \infty} \binom{K}{x}
\frac{
    \frac{M}{N}(\frac{M}{N}-1)\cdots(\frac{M}{N}-(\frac{x-1}{N}))
    (1-\frac{M}{N})(1-\frac{M}{N}-\frac{1}{N})\cdots(1-\frac{M}{N}-(\frac{K-x-1}{N}))
}{
    1(1-\frac{1}{N})\cdots(1-(\frac{K-1}{N}))
}\\
&= \binom{K}{x}p^x(1-p)^{K-x}
\end{align}
$$

よって二項分布に収束することが示された．

## 参考文献

- [久保川 達也．現代数理統計学の基礎．共立出版．](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
