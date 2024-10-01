---
title: "git 直前のコミットをなかったことする方法"
emoji: "🙆"
type: "tech"
topics: []
published: false
---



```bash
git reset --soft HEAD^
```

で直前のcommitをなかったことにし，そのcommitでコミットされた内容をステージングエリアに戻すことができます．
