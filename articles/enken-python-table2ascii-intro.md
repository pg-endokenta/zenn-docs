---
title: "Discordに表形式のデータを綺麗に送信したい"
emoji: "🎸"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["python", "discord"]
published: true
---

## はじめに

私が属しているコミュニティでは，コミュニケーションツールとしてDiscordを利用しています．
そのDiscord内にPythonで作成したBotを導入しており，そのBotは

- ボイスチャンネルの滞在時間をランキング形式で通知
- リアクシション数をランキング形式で通知

ということを行なっています．

ランキングは順位，ユーザー名，結果，前日比の項目からなる表形式のデータです．

現状そのBotが出力するランキング結果の形式が無骨であると感じるため，表形式のデータをDiscordで綺麗に表示する方法を探していました．

DiscordではMarkdown形式でメッセージを装飾できる機能があるのですが，Markdownの表には対応していません．([参考](https://support.discord.com/hc/en-us/articles/210298617-Markdown-Text-101-Chat-Formatting-Bold-Italic-Underline))

そこで，他に何か良い方法がないか調べたところ，`table2ascii`というPythonライブラリを見つけました．

## どのように解決されたのか

`table2ascii`は，リスト形式でデータを受け取り，それを綺麗な表形式の文字列に変換してくれるライブラリです．

このライブラリによって出力された文字列を`コードブロック`としてDiscordに送信することで，綺麗な表形式のデータを表示することができました．

:::message
横幅に余裕のあるPCでは綺麗に表示されるのですが，スマートフォンなどの狭い画面では表示が崩れました．
:::

:::message
日本語を使用してもレイアウトが崩れました．
:::

以下がBeforeとAfterの比較です．

### Before

![変更前のランキングの画像](https://storage.googleapis.com/zenn-user-upload/728e5b5d8618-20241017.png)

### After

![変更後のランキングの画像](https://storage.googleapis.com/zenn-user-upload/a6fce2ee1f28-20241017.png)

## table2asciiの簡単な使い方の説明

`table2ascii`を使用する簡単なサンプルは以下です．

まずインストールを行います． ([PyPI](https://pypi.org/project/table2ascii/))

```bash
pip install table2ascii
```

サンプルのpythonコードは以下です．

```python
from table2ascii import table2ascii

output = table2ascii(
    header=["Rank", "Username", "Reactions", "Change"],
    body=[["1", "user1", "40", "3"], ["2", "user2", "20", "2"]],
)

text = f"```\n{output}\n```"
```

`table2ascii`関数には`header`と`body`のような引数として，リスト型でデータを渡すことができ，表形式の文字列として返してくれます．

最後のtext変数は，`output`をmarkdown形式におけるコードブロックとして囲んだことを意味する文字列を格納しています．これをDiscordに送信することで綺麗な表形式のデータとして表示することができます．

今回扱っていませんが，数種類のスタイルを選択することもできます．
簡単なサンプルは[こちら](https://table2ascii.readthedocs.io/en/stable/usage.html#convert-lists-to-ascii-tables)から確認できます．

## 参考

- [tale2ascii 公式ドキュメント](https://table2ascii.readthedocs.io/en/stable/index.html)
