---
title: "pythonでラングフォード方程式のアトラクタを描画する"
emoji: "🐊"
type: "tech"
topics: ["python"]
published: true
publication_name: "ka_projects"
---

## はじめに

ラングフォード方程式のアトラクタをpython描画する機会がありました．

この記事には，

- 使用したコード
- 簡単な説明を

記載しています．

## コードの説明

以下が全体のコードです．

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# ラングフォード方程式の定義
def langford(t, state, alpha, beta, gamma, omega, rho, epsilon):
    """Langford Attractor Dynamics"""
    x, y, z = state
    dxdt = (z - beta) * x - omega * y
    dydt = omega * x + (z - beta) * y
    dzdt = gamma + alpha * z - z**3 / 3 - (x**2 + y**2) * (1 + rho * z) + epsilon * z * x**3
    return [dxdt, dydt, dzdt]

def solve_langford(initial_state, t_span, t_eval, params):
    """Solve Langford Attractor equations"""
    alpha, beta, gamma, omega, rho, epsilon = params
    solution = solve_ivp(
        langford, t_span, initial_state, args=params, t_eval=t_eval, method='RK45'
    )
    return solution

def plot_langford(solution, skip=1000, title="Langford Attractor"):
    """Plot the solution of Langford Attractor"""
    # Skip initial transients
    x, y, z = solution.y
    x, y, z = x[skip:], y[skip:], z[skip:]

    # Create 3D plot
    fig = plt.figure(figsize=(10, 7))
    ax = fig.add_subplot(111, projection='3d')
    ax.plot(x, y, z, lw=0.5)
    ax.set_title(title, fontsize=14)
    ax.set_xlabel("X axis")
    ax.set_ylabel("Y axis")
    ax.set_zlabel("Z axis")
    plt.show()

if __name__ == "__main__":
    # パラメータ設定
    params = (1.0, 0.7, 0.6, 3.5, 0.25, 0)  # alpha, beta, gamma, omega, rho, epsilon

    # 初期条件と時間範囲
    initial_state = [1.0, 1.0, 1.0]  # x0, y0, z0
    t_span = (0, 200)  # 時間の範囲
    t_eval = np.linspace(t_span[0], t_span[1], 20000)  # 描画用のタイムステップ

    # 数値積分
    solution = solve_langford(initial_state, t_span, t_eval, params)

    # 描画
    plot_langford(solution, skip=1000)
```

### ラングフォード方程式の定義

```python
def langford(t, state, alpha, beta, gamma, omega, rho, epsilon):
    """Langford Attractor Dynamics"""
    x, y, z = state
    dxdt = (z - beta) * x - omega * y
    dydt = omega * x + (z - beta) * y
    dzdt = gamma + alpha * z - z**3 / 3 - (x**2 + y**2) * (1 + rho * z) + epsilon * z * x**3
    return [dxdt, dydt, dzdt]
```

ここではラングフォード方程式を定義しています．
`solve_ivp`関数を用いて数値積分を行うため，引数は`(t, state, <パラメータ>)`としています．

### 数値積分

```python
def solve_langford(initial_state, t_span, t_eval, params):
    """Solve Langford Attractor equations"""
    alpha, beta, gamma, omega, rho, epsilon = params
    solution = solve_ivp(
        langford, t_span, initial_state, args=params, t_eval=t_eval, method='RK45'
    )
    return solution
```

`solve_ivp`関数を用いて，ラングフォード方程式を数値的に解いています．

### 描画

```python
def plot_langford(solution, skip=1000, title="Langford Attractor"):
    """Plot the solution of Langford Attractor"""
    # Skip initial transients
    x, y, z = solution.y
    x, y, z = x[skip:], y[skip:], z[skip:]

    # Create 3D plot
    fig = plt.figure(figsize=(10, 7))
    ax = fig.add_subplot(111, projection='3d')
    ax.plot(x, y, z, lw=0.5)
    ax.set_title(title, fontsize=14)
    ax.set_xlabel("X axis")
    ax.set_ylabel("Y axis")
    ax.set_zlabel("Z axis")
    plt.show()
```

`matplotlib`を用いて，ラングフォード方程式のアトラクタを描画しています．

### 実行部分

```python
if __name__ == "__main__":
    # パラメータ設定
    params = (1.0, 0.7, 0.6, 3.5, 0.25, 0)  # alpha, beta, gamma, omega, rho, epsilon

    # 初期条件と時間範囲
    initial_state = [1.0, 1.0, 1.0]  # x0, y0, z0
    t_span = (0, 200)  # 時間の範囲
    t_eval = np.linspace(t_span[0], t_span[1], 20000)  # 描画用のタイムステップ

    # 数値積分
    solution = solve_langford(initial_state, t_span, t_eval, params)

    # 描画
    plot_langford(solution, skip=1000)
```

パラメータ設定，初期条件の設定，数値積分，描画を行う部分です．

## 実行結果

以下が描画されたアトラクタです．

![langford](/images/enken-python-plot-langford-attractor/img1.png)
