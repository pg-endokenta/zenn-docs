---
title: "DjangoにCeleryを用いた非同期処理を追加する"
emoji: "🗂"
type: "tech"
topics: []
published: false
---

Djangoを使用しているときに，「重めの処理を開始したいけどレスポンスはすぐに返したい」という場合の解決策の一つとして「Celery」を用いることが挙げられます．

## Celeryとは

野菜のセロリと同じスペルです．
Pythonにおいて非同期処理を簡単に実装できるようにしてくれるパッケージです．
公式ドキュメント

PyPI
