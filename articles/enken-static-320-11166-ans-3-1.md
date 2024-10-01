---
title: "現代数理統計学の基礎 第3章 演習問題 問1 自作解答"
emoji: "⛳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---

確率母関数の定義より，

$$
\begin{aligned}
G_X(t) &= E[t^X] \\
\end{aligned}
$$

であり，離散一様分布の確率関数は

$$
P(X=x | N) = \frac{1}{N} \quad (x=1,2,\ldots,N)
$$
である．
よって一様分布の確率母関数は，

$$
\begin{aligned}
G_X(t) &= \sum_{x=1}^{N} t^x P(X=x|N) \\
&= \sum_{x=1}^{N} t^x \frac{1}{N} \\
&= \frac{1}{N} \sum_{x=1}^{N} t^x \\
\end{aligned}
$$
である．

平均と分散を確率母関数から求めるにはそれぞれ

$$
\begin{aligned}
E[X] &= G_X'(1) \\
\end{aligned}
$$

$$
\begin{aligned}
V[X] &= E[X(X-1)] + E[X] - E[X]^2 \\
&= G_X''(1) + G_X'(1) - G_X'(1)^2 \\
\end{aligned}
$$

と求めればよく，

$$
G_X'(t) = \frac{1}{N} \sum_{x=1}^{N} x t^{x-1} \\
G_X''(t) = \frac{1}{N} \sum_{x=1}^{N} x(x-1) t^{x-2}
$$

$$
\begin{aligned}
G_X'(1) 
&= \frac{1}{N} \sum_{x=1}^{N} x \\
&= \frac{1}{N} \frac{N(N+1)}{2} \\
&= \frac{N+1}{2}
\end{aligned}
$$

$$
\begin{aligned}
G_X''(1) 
&= \frac{1}{N} \sum_{x=1}^{N} x(x-1) \\
&= \frac{1}{N} \left( \sum_{x=1}^{N} x^2 -\sum_{x=1}^{N} x \right) \\
&= \frac{1}{N} \left( \frac{N(N+1)(2N+1)}{6} - \frac{N(N+1)}{2} \right) \\
&= \frac{(N+1)(2N+1)}{6} - \frac{N+1}{2} \\
&= \frac{N+1}{6} ((2N+1)-3) \\
&= \frac{N+1}{6} (2N-2) \\
&= \frac{(N+1)(N-1)}{3}
\end{aligned}
$$

であるから，

$$
\begin{aligned}
E[X] &= \frac{N+1}{2} \\
\end{aligned}
$$

$$
\begin{aligned}
V[X] &= \frac{(N+1)(N-1)}{3} + \frac{N+1}{2} - \left( \frac{N+1}{2} \right)^2 \\
&= \frac{(N+1)(N-1)}{3} + \frac{N+1}{2} - \frac{(N+1)^2}{4} \\
&= \frac{N+1}{12} \left( 4(N-1) + 6 - 3(N+1) \right) \\
&= \frac{N+1}{12} (4N-4+6-3N-3) \\
&= \frac{N+1}{12} (N-1) \\
&= \frac{(N+1)(N-1)}{12}
\end{aligned}
$$

となる．