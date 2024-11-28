---
title: "Pythonで簡単ローカルサーバー構築：python -m http.serverでindex.htmlを表示する方法"
emoji: "🐿"
type: "tech"
topics: ["python"]
published: true
---

## 1. はじめに

作りたいもののプロトタイプを作成する際に，WebAPIやそれを簡単にテストできるhtmlファイルをChat GPTに用意してもらうことがあります．

API側にALLOW ORIGINの設定があったため，それを含めてテスト用のhtmlファイルを簡単に表示できる方法を探していました．

その際にPythonの標準ライブラリを使って簡易サーバーを立てられるということを知ったので，その方法を紹介します．

## 2. python -m http.serverとは

簡易HTTPサーバー：Python 3に標準搭載されているモジュールで、簡単にHTTPサーバーを立ち上げることができます。([参考](https://docs.python.org/3.13/library/http.server.html))

## 3. 事前準備

Python 3がインストールされている環境と，index.htmlを用意します．

## 4. 手順

### 4.1 作業ディレクトリへ移動

index.htmlを適当なディレクトリに配置し，そのディレクトリに移動します．

```bash
cd /path/to/your/directory
```

### 4.2 サーバーを立ち上げる

以下のコマンドでサーバーを立ち上げます．

```bash
python -m http.server
```

デフォルトでは8000番ポートでサーバーが立ち上がります．

### 4.3 ブラウザでアクセス

ブラウザで以下のURLにアクセスします．

<http://localhost:8000>

## 5. ポート番号を指定する

以下のようにすることで，ポート番号を指定することができます．

```bash
python -m http.server 8080
```

## 6. ディレクトリの指定

以下のようにすることで，ルートとなるディレクトリを指定することができます．

```bash
python -m http.server --directory /path/to/your/directory
```

## 7. まとめ

Python 3が使える環境であれば，簡単にローカルサーバーを立てることができます．
今回紹介したものは簡易的なものであり，本番環境で使用することは推奨されていません．

## 参考

[http.serverのドキュメント](https://docs.python.org/3.13/library/http.server.html)
