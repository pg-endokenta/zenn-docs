---
title: "現代数理統計学 第2章 演習問題 問4 自作解答"
emoji: "👋"
type: "tech"
topics: ["統計学"]
published: true
---


## はじめに

この記事は，[現代数理統計学の基礎](https://www.kyoritsu-pub.co.jp/book/b10003681.html)の第2章演習問題の問4について自作の解答を記したものです．

問題文，解答が掲載されている公式のサイトは[こちら](https://sites.google.com/site/ktatsuya77/)です．

## 解答

### $E[(X-t)^2]$を最小にする$t$の値

$$
\begin{aligned}
E[(X-t)^2] &= E[X^2 -2tX + t^2] \\
&= E[X^2] - E[2tX] + E[t^2] \\
&= E[X^2] - 2tE[X] + t^2
\end{aligned}
$$

これを$t$の式と見ると，$t$に関する2次関数であり

$$
\begin{aligned}
E[X^2] - 2tE[X] + t^2
&= t^2  - 2E[X] t + E[X^2] \\
&= t^2  - 2E[X] t + E[X]^2 - E[X]^2 + E[X^2] \\
&= (t - E[X])^2 - E[X]^2 + E[X^2]  \\
&= (t - E[X])^2 + E[X^2] - E[X]^2 \\
&= (t - E[X])^2 + V[X]
\end{aligned}
$$

よって，$t=E[X]$のときに最小となる．

### $E[|X-t|]$を最小にする$t$の値

$$
\begin{aligned}
E[|X-t|]
&= \int_{-\infty}^{\infty} |x-t| f_X(x) dx \\
&= \int_{-\infty}^{t} -(x-t) f_X(x) dx + \int_{t}^{\infty} (x-t) f_X(x) dx \\
&= \int_{-\infty}^{t} -x f_X(x) dx + \int_{-\infty}^{t} t f_X(x) dx + \int_{t}^{\infty} x f_X(x) dx + \int_{t}^{\infty} -t f_X(x) dx\\
&= -\int_{-\infty}^{t} x f_X(x) dx + t\int_{-\infty}^{t} f_X(x) dx + \int_{t}^{\infty} x f_X(x) dx -t\int_{t}^{\infty} f_X(x) dx\\
&= -\int_{-\infty}^{t} x f_X(x) dx + \int_{t}^{\infty} x f_X(x) dx +
t\left(
    \int_{-\infty}^{t} f_X(x) dx -\int_{t}^{\infty} f_X(x) dx
\right) \\
&= - \int_{-\infty}^{t} x f_X(x) dx +
\left(
    \int_{-\infty}^{t} x f_X(x) dx
    - \int_{-\infty}^{t} x f_X(x) dx
\right) +
\int_{t}^{\infty} x f_X(x) dx +
t\left(
    \int_{-\infty}^{t} f_X(x) dx -\int_{t}^{\infty} f_X(x) dx
\right) \\
&= -2\int_{-\infty}^{t} x f_X(x) dx +
\int_{-\infty}^{t} x f_X(x) dx +
\int_{t}^{\infty} x f_X(x) dx +
t\left(
    \int_{-\infty}^{t} f_X(x) dx -\int_{t}^{\infty} f_X(x) dx
\right) \\
&= -2\int_{-\infty}^{t} x f_X(x) dx +
E[X] +
t\left(
    \int_{-\infty}^{t} f_X(x) dx -\int_{t}^{\infty} f_X(x) dx
\right) \\
&= -2\int_{-\infty}^{t} x f_X(x) dx +
E[X] +
t\left(
    \int_{-\infty}^{t} f_X(x) dx -\int_{t}^{\infty} f_X(x) dx +
    \left(
        \int_{-\infty}^{t} f_X(x) dx -\int_{-\infty}^{t} f_X(x) dx
    \right)
\right) \\
&= -2\int_{-\infty}^{t} x f_X(x) dx +
E[X] +
t\left(
    2\int_{-\infty}^{t} f_X(x) dx -
    \left(
        \int_{-\infty}^{t} f_X(x) dx + \int_{t}^{\infty} f_X(x) dx
    \right)
\right) \\
&= -2\int_{-\infty}^{t} x f_X(x) dx +
E[X] +
t\left(
    2\int_{-\infty}^{t} f_X(x) dx - 1
\right) \\
\end{aligned}
$$

これの最小値を求めるために，$t$で微分する．

$$
\begin{aligned}
\frac{d}{dt} E[|X-t|]
&= \frac{d}{dt}
\left(
    -2\int_{-\infty}^{t} x f_X(x) dx +
    E[X] +
    t\left(
        2\int_{-\infty}^{t} f_X(x) dx - 1
    \right)
\right) \\
&= -2 t f_X(t) +
\left(
        2\int_{-\infty}^{t} f_X(x) dx - 1
\right) +
t \left(
    2 f_X(t)
\right) \\
&= 2\int_{-\infty}^{t} f_X(x) dx - 1
\end{aligned}
$$

この値が0になるのは

$$
\begin{aligned}
2\int_{-\infty}^{t} f_X(x) dx - 1 &= 0 \\
\int_{-\infty}^{t} f_X(x) dx &= \frac{1}{2} \\
\end{aligned}
$$

のときである．

よって，$t$が　$\int_{-\infty}^{t} f_X(x) dx = \dfrac{1}{2}$を満たす値のとき最小となる．

## 参考文献

- [現代数理統計学の基礎 共立出版](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
