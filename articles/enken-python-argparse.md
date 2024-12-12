---
title: "pythonでコマンドライン引数を使う方法（入門）"
emoji: "🦭"
type: "tech"
topics: ["python"]
published: true
---

## はじめに

Pythonでコマンドライン引数を指定してプログラムを実行したい場合があります．

Pythonの標準ライブラリには，コマンドライン引数を処理するための`argparse`モジュールが用意されています．

今回は，`argparse`モジュールの簡単な使い方について説明します．

## argparseモジュールの簡単な使い方

以下がサンプルコードです．

```python:example.py
import argparse

# ArgumentParserの例を作成
parser = argparse.ArgumentParser(description="Example script")

# オプションの設定
parser.add_argument("name", type=str, help="Your name")
parser.add_argument("--age", type=int, help="Your age", default=18)
parser.add_argument("--verbose", action="store_true", help="Enable verbose output")

# オプションの解釈
args = parser.parse_args()

print(f"Hello, {args.name}! You are {args.age} years old.")
if args.verbose:
    print("Verbose mode is enabled.")
```

上記のスクリプトは，`name`という必須の引数と，`age`と`verbose`というオプション引数を受け取ります．

例えば，以下のように実行すると，

```sh
python example.py Alice --age 20 --verbose
```

次のような出力が得られます．

```text
Hello, Alice! You are 20 years old.
Verbose mode is enabled.
```

### ヘルプの表示

`--help`オプションを指定すると，どのような引数が受け付けられるかを確認できます．

```sh
python example.py --help
```

上記のコマンドを実行すると，以下のようなヘルプが表示されます．

```text
usage: example.py [-h] [--age AGE] [--verbose] name

Example script

positional arguments:
  name        Your name

options:
  -h, --help  show this help message and exit
  --age AGE   Your age
  --verbose   Enable verbose output
```

### おまけ

オプションのコマンドライン引数は指定する際に，`--`の後のオプション名を短くして指定することもできます．

例

```sh
python3 example.py Alice --a 20 --v
```

## 参考

- argparseモジュールの情報：[公式ドキュメント](https://docs.python.org/3/library/argparse.html)
