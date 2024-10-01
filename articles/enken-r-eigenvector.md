---
title: "【R】 行列の固有ベクトルの求め方"
emoji: "🕌"
type: "tech"
topics:
  - "r"
published: true
published_at: "2024-09-26 12:30"
---


Rにおいて行列の固有ベクトルは以下の手順で求められる．

```r: sample.R
# 行列を生成
A <- matrix(c(1,2,3,4,5,6,7,8,9), 3, 3, TRUE)

# 関数eigen()を用いて固有値(values)と固有ベクトル(vectors)が含まれるリストを作成
# eigen_Aに代入
eigen_A <- eigen(A)

# 固有ベクトルを表示
eigen_A$vectors

```

関数eigen()の情報：[公式ドキュメント](https://cran.r-project.org/doc/manuals/r-release/fullrefman.pdf)のp.176