---
title: "Git Submodulesの使い方"
emoji: "🙆"
type: "tech"
topics: ["git"]
published: true
---


## submodulesとは

gitを使用してプロジェクトを管理しているときに，ほかのプロジェクトを取り込みたい場合があります．

そのようなときに使用できるのがSubmodulesです．

Submodulesを使用することで，あるGitリポジトリを別のGitリポジトリのサブディレクトリとして扱うことができます．

特定のバージョンの外部プロジェクトを安全に参照しつつ管理できるというメリットがあります．

## submoduleの追加

submoduleを追加するには，以下のコマンドを実行します．

```bash
git submodule add <url> <path>
```

`<url>`には追加したいリポジトリのURLを指定し，
`<path>`には追加したいディレクトリ名を指定します．
`<path>`が空欄の場合は，追加するリポジトリ名がそのままディレクトリ名になります．

このコマンドを実行すると.gitmodulesというファイルが作成されます．
このファイルにはsubmoduleの情報が記載されています．

submoduleは特定のコミットを指し示すようになっています．

## submoduleを含むリポジトリのclone

submoduleを含むリポジトリをcloneするには，以下のコマンドを実行します．

```bash
git clone --recurse-submodules <url>
```

`--recurse-submodules`オプションをつけることで，submoduleも一緒にcloneされます．

`--recurse-submodules`オプションをつけずにcloneした場合は，

```bash
git submodule init
git submodule update
```

を実行することでsubmoduleを取得することができます．

## submoduleの更新

submoduleの更新を行うには，submoduleのディレクトリに移動し，以下のコマンドを実行します．(submoduleのmainブランチの内容を取得する場合)

```bash
git fetch
git merge origin/main
```

または，submoduleのディレクトリに移動しなくても以下のコマンドを実行することで更新ができます．

```bash
git submodule update --remote
```

デフォルトでは，リモートsubmoduleリポジトリのdefault branchの内容が取得されます．

これはすべてのsubmoduleを更新するため，特定のsubmoduleのみを更新したい場合は以下のコマンドを実行します．

```bash
git submodule update --remote <path>
```

`<path>`には更新したいsubmoduleのディレクトリ名を指定します．

## 他の人がsubmoduleを更新した場合

誰かがsubmoduleが指し示すコミットを更新した場合，git pullを実行するだけではsubmoduleの更新があることのみが分かり，submoduleのファイル自体の更新は行われません．

submoduleを最新の状態にするには，以下のコマンドを実行します．

```bash
git submodule update --init --recursive
```

`--init`と`--recursive`が必要ない場合もありますが，一応つけておくと安心です．

## おわりに

今回はsubmoduleの簡単な使い方について説明しました．

## 参考

- [7.11 Git Tools - Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
