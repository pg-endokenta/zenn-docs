---
title: "浮動小数点の誤差を考慮したPythonの配列比較方法"
emoji: "🐨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["統計学"]
published: false
---


## 書くこと

この記事では，浮動小数点の誤差を考慮してPythonの配列を比較する方法について書いています．具体的には

- numpyの`allclose`関数と使い方
- 許容範囲に対する誤差

について書いています．

## はじめに

浮動小数点の計算には誤差が生じることがあります．
そのため，同じ値だと考えられるものでも，プログラムにおいては異なる値として扱われることがあります．
具体的には以下の例が上げられます．

```python
import numpy as np

array1 = np.array([0.1 + 0.2, 0.3 + 0.3])
array2 = np.array([0.3, 0.6])

print(array1 == array2)
## 出力
# [False  True]
```

誤差が生じることにより，うまく比較をできていないことが分かります．

浮動小数を含む配列同士の比較を行う方法として，`numpy`の`allclose`関数があります．
この関数は誤差を許容して配列を比較できます．

## numpyの`allclose`関数と使い方

`numpy.allclose`関数は二つの配列の各要素が許容範囲内で等しい場合に`True`を返します．

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

### 許容範囲に対する誤差

誤差を許容して比べる場合に，その許容する誤差の近くでは結果に誤差が生じる可能性があります．

同じ相対誤差でも，微量の誤差により結果が異なる場合を以下に示します．

例

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

このようにどちらも差は`0.01`以下で，`allclose`関数で0.01以下を許容しているにもかかわらず，`a_1`と`b_1`の比較では`False`が返されます．

このようになる理由は`1.010 - 1.000` の結果に誤差が含まれるためだと考えられます．

```python
print(1.010 - 1.000)
print((1.010 - 1.000) == 0.01)
## 出力
# 0.010000000000000009
# False
```

不要な部分の切り捨てを行うことで，上記のような場合でも出力をそろえることができます．
具体例は以下

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

## まとめ

浮動小数点の誤差を考慮して配列を比較する方法について説明しました．

`numpy`の`allclose`関数については浮動小数点の計算により生じた誤差を考慮するために使用することができるとともに，それ以外の用途で使用する場合には

- 誤差の許容範囲に余裕を持たせる．
- 目的に合わせて適切に使用する．

ことが大切です．

## 参考

- [numpy allclose](https://numpy.org/doc/stable/reference/generated/numpy.allclose.html)
