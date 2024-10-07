---
title: "gitで使用するエディターを変更する方法
emoji: "🚗"
type: "tech"
topics:
  - "git"
published: true
---


## 書くこと

`commit`を行う際などにコミットメッセージなどを入力するためにエディターが開くことがある．
ことのきに使用するエディターを指定する方法について説明する．

## 知っておくと良いこと

エディターを設定する場所はいくつか存在し，その優先順位は以下のようになっている．[(参考)](https://git-scm.com/docs/git-var#Documentation/git-var.txt-GITEDITOR)

1. `$GIT_EDITOR`環境変数
2. `core.editor`設定
3. `$VISUAL`環境変数
4. `$EDITOR`環境変数

## 方法

今回は2番目の`core.editor`設定を変更する方法について説明する．

core.editor設定を変更するには以下のコマンド

```bash
git config --global core.editor <エディタ名>
```

を実行すれば良い．

例えばvimを使用したい場合は

```bash
git config --global core.editor "vim --nofork"
```

とすれば良い．

その他の主なエディターについて，どのような値を設定すれば良いかは[こちら](https://git-scm.com/book/en/v2/Appendix-C:-Git-Commands-Setup-and-Config#ch_core_editor)から確認できる．
