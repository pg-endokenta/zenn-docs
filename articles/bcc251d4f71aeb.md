---
title: "現代数理統計学 第2章 演習問題 問4 自作解答"
emoji: "👋"
type: "tech"
topics: []
published: false
---

### $E[(X-t)^2]$の最小値

$$
\begin{align*}
E[(X-t)^2] &= E[X^2 -2tX + t^2] \\
&= E[X^2] - E[2tX] + E[t^2] \\
&= E[X^2] - 2tE[X] + t^2
\end{align*}
$$

これを$t$の式と見ると，

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

であり，$t=E[X]$のとき最小値を取ることがわかる．


### $E[|X-t|]$の最小値