---
title: "SSHをスマートに，SSH Configの書き方(初級)"
emoji: "🦤"
type: "tech"
topics: ["ssh"]
published: true
---

## はじめに

SSH接続する際には

- ユーザー名
- ホスト名
- ポート番号
- 鍵ファイルのパス

等の情報が必要になります．

これらの情報を毎回入力するのは面倒です．

SSH接続において，この面倒を解消する方法の一つとして，SSH Configファイルを利用する方法があります．

Configファイルに接続情報を書いておくと，

```sh
ssh <好きな名前>
```

のような，短いコマンドでSSH接続できるようになります．

## SSH Configファイルとは

SSH Configファイルは，SSH接続の設定を記述しておけるファイルです．
通常は`~/.ssh/config`に配置します．

## SSH Configファイルの書き方

基本的な構文は以下のようになります．

```text
Host <好きな名前>
    HostName <ホスト名 or IPアドレス>
    User <ユーザー名>
    Port <ポート番号>
    IdentityFile <鍵ファイルのパス>
```

具体的には

```text
Host example
    HostName example.com
    User user
    Port 22
    IdentityFile ~/.ssh/id_rsa
```

のように書くと，以下の二つのコマンドは同じ意味になります．

```sh
ssh user@example.com -p 22 -i ~/.ssh/id_rsa
```

```sh
ssh example
```

## 複数の接続情報を書く

複数の接続情報を書く際は，以下のように書きます．

```text
Host example1
    HostName example1.com
    User user1
    Port 22
    IdentityFile ~/.ssh/id_rsa

Host example2
    HostName example2.com
    User user2
    Port 22
    IdentityFile ~/.ssh/id_rsa
```

## ポートフォワーディングの設定

Configファイルにポートフォワーディングの設定を書くこともできます．

```text
Host example
    HostName example.com
    User user
    Port 22
    IdentityFile ~/.ssh/id_rsa
    LocalForward 8080 localhost:80
```

以上のように書くと，
ローカルマシンの`localhost:8080`へのアクセスが
リモートマシンの`example.com:80`へのアクセスになります．

## まとめ

この他にも

- ワイルドカードの利用
- いろいろなオプションの設定

を行うことができます．

何ができるかは

```sh
man ssh_config
```

または

[OpenSSH マニュアルページ ssh_config](https://man.openbsd.org/ssh_config)

で確認できます．

## おまけ

Host以降のHostNameなどのインデントは必須ではありません．

そのため，

```text
Host example
HostName example.com
User user
Port 22
IdentityFile ~/.ssh/id_rsa
```

のように書いても問題ありません．
