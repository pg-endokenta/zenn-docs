---
title: "【Python】浮動小数点の計算による誤差とnumpy.allcloseを用いた誤差を考慮した配列比較"
emoji: "🐨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["python", "numpy"]
published: true
---

## はじめに

浮動小数点の計算では誤差が生じることがあります．
そのため，同じ値だと考えられるものでも，プログラム上では等しくないものとして扱われることがあります．
具体的な例は以下です

```python
import numpy as np

array1 = np.array([0.1 + 0.2, 0.3 + 0.3])
array2 = np.array([0.3, 0.6])

print(array1 == array2)
## 出力
# [False  True]
```

どちらの`array`も1つ目の要素が$0.3$, 2つ目の要素が$0.6$であり，それぞれ等しいように見えます．しかし，計算時に誤差が生じるため，片方が等しくないと判定されています．

このような誤差を考慮し，浮動小数点を含む配列同士の比較を行う方法として，`numpy`の`allclose`関数があります．

この関数は指定した誤差を許容して配列を比較できます．

## numpyの`allclose`関数と使い方

`numpy.allclose`関数は2つの配列の各要素が許容範囲内で等しい場合に`True`を返します．

具体的には以下のように使用します．

```python
import numpy as np

a = np.array([0.1, 0.2, 0.3])
b = np.array([0.1, 0.1 + 0.1, 0.1 + 0.2])

result = np.allclose(a, b)
print(result)
## 出力
# True
```

`allclose`関数は次のような引数を持ちます.
`numpy.allclose(a, b, atol=1e-8, rtol=1e-5, equal_nan=False)`

- `a` : 比較する配列1
- `b` : 比較する配列2
- `atol` : 許容される絶対誤差 (デフォルトは`1e-8`)
- `rtol` : 許容される相対誤差 (デフォルトは`1e-5`)
- `equal_nan` : `True`の場合，`NaN`を等しいとみなす (デフォルトは`False`)

Trueを返す条件は，各要素に対して次の条件が成り立つ場合です．

```python
absolute(a - b) <= (atol + rtol * absolute(b))
```

ここから分かる通り，`allclose(a, b)`　と `allclose(b, a)` が異なる結果を返す場合があります．

無理やり例を作るとすると，次のような場合です．

```python
a = np.array([1.0])
b = np.array([2.0])
print(np.allclose(a, b, atol=0, rtol=0.5))
print(np.allclose(b, a, atol=0, rtol=0.5))
## 出力
# True
# False
```

使用する場合は，`atol`と`rtol`の値を適切に設定することが重要です．

パラメータ`equal_nan`についてはNaN同士を等しいとみなすかどうかを指定する引数です．デフォルトでは`False`であり，`NaN`同士は等しくないと判定されます．

```python
import math
import numpy as np

nan_array_1 = np.array([math.nan, math.nan, np.nan, np.nan])
nan_array_2 = np.array([math.nan, np.nan, math.nan, np.nan])

print(np.allclose(nan_array_1, nan_array_2))
print(np.allclose(nan_array_1, nan_array_2,  equal_nan=True))
## 出力
# False
# True
```

### 差を調べるために使うときは誤差に注意すること

`allclose`関数の性質より，2つの配列の各要素間の差が許容範囲内かどうかを判定することに使いたいと考えるかもしれません．このときに，誤差の存在を忘れないことが重要です．以下に具体例として，2つの配列の各要素の差が0.01以下か調べたい場合に，誤差により結果に差が生じる例を示します．

```python
# 差は0.01以下
a_0 = np.array([0.008, 0.009, 0.010])
b_0 = np.array([0.000, 0.000, 0.000])

# こちらも差は0.01以下
a_1 = np.array([1.008, 1.009, 1.010])
b_1 = np.array([1.000, 1.000, 1.000])

# 絶対誤差0.01以下まで許容する
print(np.allclose(a_0, b_0, atol=0.01, rtol=0))
print(np.allclose(a_1, b_1, atol=0.01, rtol=0))
## 出力
# True
# False
```

このようになる理由は$1.010 - 1.000$ の結果に誤差が含まれるためです．

```python
print(1.010 - 1.000)
print((1.010 - 1.000) <= 0.01)
## 出力
# 0.010000000000000009
# False
```

`allclose`関数を使用する上では

- 許容する誤差には余裕を持たせる
- 誤差について適切に考慮する

ことが重要です．

### 差の比較例

上で上げた例の続きとして，差が0.01以下であるかを誤差を考量して確認する方法の一例を示します．差を取り，不要な桁の切り捨てを行うと，誤差を考慮した比較が可能です．

```python
# 差は0.01以下
a_0 = np.array([0.008, 0.009, 0.010])
b_0 = np.array([0.000, 0.000, 0.000])
# 差の配列
c_0 = a_0 - b_0
# 小数第3位を切り捨て
d_0 = np.trunc(c_0 * 100) / 100

# こちらも差は0.01以下
a_1 = np.array([1.008, 1.009, 1.010])
b_1 = np.array([1.000, 1.000, 1.000])
c_1 = a_1 - b_1
d_1 = np.trunc(c_1 * 100) / 100

# 絶対誤差0.01以下まで許容する
print("差をとったものに対して確認")
print(np.all(c_0 <= 0.01))
print(np.all(c_1 <= 0.01))

print("切り捨てたものに対して確認")
print(np.all(d_0 <= 0.01))
print(np.all(d_1 <= 0.01))
## 出力
# 差をとったものに対して確認
# True
# False
# 切り捨てたものに対して確認
# True
# True
```

## 参考

- [numpy.allcloseのドキュメント](https://numpy.org/doc/stable/reference/generated/numpy.allclose.html)
