---
title: "現代数理統計学の基礎 第3章 演習問題 問2 自作解答"
emoji: "⛳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学"]
published: true
---


## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第3章演習問題の問2について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/)です．

## 解答

### 2項係数の関係式1

$\dbinom{n}{k} = \dbinom{n}{n-k}$が成り立つことを示す．

$$
\begin{aligned}
(左辺)
&= \binom{n}{k} \\
&= \frac{n!}{k!(n-k)!} \\
\end{aligned}
$$

$$
\begin{aligned}
(右辺)
&= \binom{n}{n-k} \\
&= \frac{n!}{(n-k)!(n-(n-k))!} \\
&= \frac{n!}{(n-k)!k!} \\
&= \frac{n!}{k!(n-k)!} \\
\end{aligned}
$$

よって(左辺) = (右辺)であり，$\dbinom{n}{k} = \dbinom{n}{n-k}$が成り立つことが示された．

### 2項係数の関係式2

$\dbinom{n+1}{k} = \dbinom{n}{k-1} + \dbinom{n}{k}$が成り立つことを示す．

$$
\begin{aligned}
(左辺)
&= \binom{n+1}{k} \\
&= \frac{(n+1)!}{k!(n+1-k)!} \\
&= \frac{(n+1)!}{k!(n-k+1)!} \\
\end{aligned}
$$

$$
\begin{aligned}
(右辺)
&= \binom{n}{k-1} + \binom{n}{k} \\
&= \frac{n!}{(k-1)!(n-(k-1))!} + \binom{n}{k} \\
&= \frac{n!}{(k-1)!(n-k+1)!} + \binom{n}{k} \\
&= \frac{kn!}{k!(n-k+1)!} + \binom{n}{k} \\
&= \frac{kn!}{k!(n-k+1)!} + \frac{n!}{k!(n-k)!} \\
&= \frac{kn!}{k!(n-k+1)!} + \frac{(n-k+1)n!}{k!(n-k+1)!} \\
&= \frac{kn! + (n-k+1)n!}{k!(n-k+1)!} \\
&= \frac{(k+n-k+1)n!}{k!(n-k+1)!} \\
&= \frac{(n+1)n!}{k!(n-k+1)!} \\
&= \frac{(n+1)!}{k!(n-k+1)!} \\
\end{aligned}
$$

よって(左辺) = (右辺)であり，$\dbinom{n+1}{k} = \dbinom{n}{k-1} + \dbinom{n}{k}$が成り立つことが示された．

### 数学的帰納法を用いて2項定理を証明する

2項定理

$$
(a+b)^n = \sum_{k=0}^{n} \binom{n}{k} a^{k} b^{n-k}
$$
が成り立つことを数学的帰納法を用いて証明する．

#### $n=1$の場合

$$
\begin{aligned}
(左辺)
&= (a+b)^1 \\
&= a+b
\end{aligned}
$$

$$
\begin{aligned}
(右辺)
&= \sum_{k=0}^{1} \binom{1}{k} a^{k} b^{1-k} \\
&= \binom{1}{0} a^{0} b^{1-0} + \binom{1}{1} a^{1} b^{1-1} \\
&= b + a \\
&= a + b
\end{aligned}
$$

(左辺) = (右辺)であり，成り立つ．

#### $n=t$の時に成り立つと仮定したときの$n=t+1$の場合

$$
\begin{aligned}
(左辺)
&= (a+b)^{t+1} \\
&= (a+b)(a+b)^t \\
&= (a+b) \sum_{k=0}^{t} \binom{t}{k} a^{k} b^{t-k} \\
&= \sum_{k=0}^{t} \binom{t}{k} a^{k+1} b^{t-k} + \sum_{k=0}^{t} \binom{t}{k} a^{k} b^{t-k+1} \\
&= \sum_{k'=1}^{t} \binom{t}{k'-1} a^{k'} b^{t-k'+1} + \sum_{k=0}^{t} \binom{t}{k} a^{k} b^{t-k+1} \\
&= \sum_{k=1}^{t+1} \binom{t}{k-1} a^{k} b^{t-k+1} + \sum_{k=0}^{t} \binom{t}{k} a^{k} b^{t-k+1} \\
&= a^{t+1} + \sum_{k=1}^{t} \binom{t}{k-1} a^{k} b^{t-k+1} + \sum_{k=0}^{t} \binom{t}{k} a^{k} b^{t-k+1} \\
&= a^{t+1} + \sum_{k=1}^{t} \binom{t}{k-1} a^{k} b^{t-k+1} + \sum_{k=1}^{t} \binom{t}{k} a^{k} b^{t-k+1} + b^{t+1} \\
&= a^{t+1} + \sum_{k=1}^{t} \left( \binom{t}{k-1} + \binom{t}{k} \right) a^{k} b^{t-k+1} + b^{t+1} \\
&= a^{t+1} + \sum_{k=1}^{t} \binom{t+1}{k} a^{k} b^{t-k+1} + b^{t+1} \\
&= \sum_{k=t+1}^{t+1} \binom{t+1}{k} a^{k} b^{t-k+1} + \sum_{k=1}^{t} \binom{t+1}{k} a^{k} b^{t-k+1} + b^{t+1} \\
&= \sum_{k=t+1}^{t+1} \binom{t+1}{k} a^{k} b^{t-k+1} + \sum_{k=1}^{t} \binom{t+1}{k} a^{k} b^{t-k+1} + \sum_{k=0}^{0} \binom{t+1}{k} a^{k} b^{t-k+1} \\
&= \sum_{k=0}^{t+1} \binom{t+1}{k} a^{k} b^{t-k+1} \\
&= (右辺)
\end{aligned}
$$

よって$n=t$で成り立つと仮定したとき，$n=t+1$でも成り立つことが示された．

以上の結果より，数学的帰納法により2項定理が成り立つことが示された．

## 参考文献

- [久保川 達也．現代数理統計学の基礎．共立出版．](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
- [水町龍一．基礎数学．学術図書出版社．](https://www.gakujutsu.co.jp/product/978-4-87361-246-1/)
