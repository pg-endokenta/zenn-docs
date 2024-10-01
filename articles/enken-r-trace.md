---
title: "【R】 行列のトレースの求め方"
emoji: "🏃"
type: "tech"
topics:
  - "r"
published: true
---




## 行列のトレースの求め方

Rにおいて行列のトレースは，

1. `diag()`関数を用いて対角成分を取得
1. `sum()`関数を用いて合計を計算

を行うことによって求められる．
コード例は以下

```r
# 行列を生成
A <- matrix(c(1,2,3,4,5,6,7,8,9), 3, 3, TRUE)
A

# トレースを求める
sum(diag(A))

## 出力結果
# > # 行列を生成
# > A <- matrix(c(1,2,3,4,5,6,7,8,9), 3, 3, TRUE)
# > A
#      [,1] [,2] [,3]
# [1,]    1    2    3
# [2,]    4    5    6
# [3,]    7    8    9
# > # 対角成分を取得
# > d <- diag(A)
# > d
# [1] 1 5 9
# > # 合計を計算
# > sum(d)
# [1] 15
```

## 参考

- diag()関数の情報：[公式ドキュメント](https://stat.ethz.ch/R-manual/R-devel/library/base/html/diag.html)のp.153
- sum()関数の情報：[公式ドキュメント](https://stat.ethz.ch/R-manual/R-devel/library/base/html/sum.html)のp.583
