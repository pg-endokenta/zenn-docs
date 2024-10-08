---
title: "別のGitHubのリポジトリにコードを移す方法"
emoji: "🚥"
type: "tech"
topics:
  - "git"
published: true
published_at: "2024-09-10 19:49"
---

## 状況

現状GitHubにリポジトリを置いていて（リモートAとする），ローカルにクローンして作業している．
そのコードを別のGitHubのリポジトリ（リモートBとする）で管理したくなった．

## 方法

mainブランチを対象とする場合．
GitHubで移行先のリポジトリ（リモートB）は既に作成しているとする．
以下はすべてローカル側での作業となる

## 新しいリモートリポジトリ(リポジトリB)をローカルに知らせる．

```bash
git remote -v
```

で現在のリモートAをローカル側のgitでどのような名前で登録しているか確認する(多分origin)

次に，
`<shortname>`：使われていない名前（リモートAがoriginという名前ならそれ以外）
<`url>：<https://github.com/><ユーザー名とか>/<リポジトリBの名前>.git`みたいなやつ．
を用いて

```bash
git remote add <shortname> <url> 
```

を実行することで，リモートBを`<shortname>`という名前でローカルに認識させることができる．

きちんと追加されているかは`git remote -v`で確認できる

## ローカルの状態を最新にする

:::message
リモートBにpushする前にリモートAの最新の変更をローカルに持ってくるために行う.
リモートBへの移行において必ず必要なわけではない．
:::

```bash
git checkout main
```

でmainに移動し，

```bash
git pull
```

でローカルの状態を最新にする．

## 新しいリモートにpush

```bash
git push <shortname> main
```

これで新しい方のmainブランチにコードがpushされる.

以上の流れで新しい方のリモートリポジトリ(リポジトリB)にコードを移動することができる．
