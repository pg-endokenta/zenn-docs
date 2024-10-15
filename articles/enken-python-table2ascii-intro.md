---
title: "BotがDiscordに送信する表形式のデータを綺麗にしたい"
emoji: "🎸"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["python", "discord"]
published: false
---

## はじめに

私が属しているコミュニティでは，コミュニケーションツールとしてDiscordを利用しています．
そのDiscord内にPythonで作成したBotを導入しており，そのBotは

- ボイスチャンネルの滞在時間をランキング形式で通知
- リアクシション数をランキング形式で通知

ということを行なっています．

現状そのBotが出力するランキング結果の形式が無骨であると感じるため，ランキングを綺麗に通知したいと考えました．

ランキングは順位，ユーザー名，結果，前日比の項目からなる表形式のデータのため，この表形式のデータをDiscordで綺麗に表示する方法を探していました．

DiscordではMarkdown形式でメッセージを装飾できる機能があるのですが，Markdownの表には対応していません．([参考](https://support.discord.com/hc/en-us/articles/210298617-Markdown-Text-101-Chat-Formatting-Bold-Italic-Underline))

そこで，他に何か良い方法がないか調べたところ，`table2ascii`というPythonライブラリを見つけました．

## どのように解決されたのか

`table2ascii`は，リスト形式でデータを受け取り，それを綺麗な表形式の文字列に変換してくれるライブラリです．

このライブラリによって出力された文字列をDiscordにMarkdownのコードブロックとして送信することで，綺麗な表形式のデータを表示することができました．

:::message
横幅に余裕のあるPCでは綺麗に表示されるのですが，スマートフォンなどの狭い画面では表示が崩れました．
文字列である以上しょうがないのかなと思います．
:::

以下がBeforeとAfterの比較です．

## table2asciiの簡単な使い方の説明

`table2ascii`を使用する簡単なサンプルは以下です．

まずインストールを行います．

```bash
pip install table2ascii
```

サンプルのpythonコードは以下です．

```python
from table2ascii import table2ascii

output = table2ascii(
    header=["Rank", "Username", "Reactions", "Change"],
    body=[["1", "user1", "40", "3"], ["2", "user2", "20", "2]],
)

text = f"```\n{output}\n```"
```

`table2ascii`関数には`header`と`body`のような引数として，リスト型でデータを渡すことができ，表形式の文字列として返してくれます．

最後のtext変数は，markdown形式として`output`をコードブロックとして囲んだことを意味する文字列を格納しており，これをDiscordに送信することで綺麗な表形式のデータとして表示することができます．

## 参考文献

- [久保川 達也．現代数理統計学の基礎．共立出版．](https://www.kyoritsu-pub.co.jp/book/b10003681.html)
