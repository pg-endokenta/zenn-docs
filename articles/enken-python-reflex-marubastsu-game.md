---
title: "Pythonでフロント Reflexでマルバツゲームを作る"
emoji: "🐦"
type: "tech"
topics: ["python", "reflex"]
published: true
---

## はじめに

`Reflex`という，Pythonでバックエンドとフロントエンドを開発できるライブラリが存在します．
[Reflexのドキュメント](https://reflex.dev/)

今回はお試しとして`Reflex`を用いて「マルバツゲーム」を作成したので，その作り方を紹介します．

サンプルコードは以下のリポジトリにあります．
@[card](https://github.com/pg-endokenta/reflex_marubatsu_game)

## 作り方

マルバツゲームを作成する手順を以下に示します．

### 環境を整える

#### ディレクトリの作成

```bash
mkdir reflex_marubatsu_game
cd reflex_marubatsu_game
```

#### 仮想環境の作成

今回は`venv`を使用して仮想環境を作成します．

```bash
python -m venv .venv
source .venv/bin/activate
```

#### Reflexのインストールとプロジェクトの作成

```bash
pip install reflex
reflex init
```

※この記事を書いている時の`reflex`のバージョンは`0.6.4`です．

どのテンプレートを使用するか聞かれるので，0を入力してEnterを押します．

#### 動作確認

```bash
reflex run
```

このコマンドを実行後， <http://localhost:3000> にアクセスし，以下のような画面が表示されれば成功です．

![初期の画面](/images/enken-python-reflex-marubastsu-game/img1.png)

### マルバツゲームを作成する

ここからはコードの解説を行います．
`Reflex`で書く内容を大きく分けると，

- 状態を管理する部分
- 画面を描画する部分
- その他の部分

の3つの部分に分けることができます．

#### その他の部分

##### import

`reflex`を`rx`という名前でimportします．

```python
import reflex as rx
```

##### 定数の定義

ゲームに使用する定数を定義します．

```python
PLAYER_A = "🙆"
PLAYER_B = "🙅"
COLOR_A = "lightblue"
COLOR_B = "lightgreen"
DEFAULT_COLOR = "CadetBlue"
```

#### Stateの定義（状態を管理する部分）

`Reflex`では`State`を使用して画面の状態を管理します．

`State`では，状態を管理したい変数と，状態を更新する関数を定義することができます．

書き方の例としては以下のようになります．

```python
class SampleState(rx.State):
    count: int = 0

    def increment(self):
        self.count += 1
```

##### マルバツゲームで管理する状態

今回は

- 盤面の状態
- 盤面の色
- 現在のプレイヤー
- 勝者
- 引き分け

の状態を管理します．

コードとしては以下のようになります．

```python
class MarubatsuState(rx.State):
    board = [""] * 9
    board_colors = [DEFAULT_COLOR] * 9
    current_player = PLAYER_A
    winner = ""
    draw = False
    ...
```

##### 状態を更新する関数

###### make_move

プレイヤーが盤面をクリックしたときに呼び出される関数です．

- クリックされたマス目にプレイヤーの記号を書き込む
- ゲームの勝敗が決まったかどうかを判定
- プレイヤーを切り替える

ということを行なっています．

```python
class MarubatsuState(rx.State):
    ...
    def make_move(self, index):
        if self.board[index] == "" and self.winner == "":
            self.board[index] = self.current_player
            if self.current_player == PLAYER_A:
                self.board_colors[index] = COLOR_A
            elif self.current_player == PLAYER_B:
                self.board_colors[index] = COLOR_B

            # 勝敗判定
            if self.check_winner():
                self.winner = self.current_player
            # 引き分け判定
            elif "" not in self.board:
                self.draw = True
            # 次のプレイヤーに切り替え
            else:
                self.switch_player()
    ...
```

##### switch_player

プレイヤーを切り替える関数です．

```python
class MarubatsuState(rx.State):
    ...
    def switch_player(self):
        self.current_player = PLAYER_B if self.current_player == PLAYER_A else PLAYER_A
    ...
```

##### check_winner

勝敗を判定する関数です．

```python
class MarubatsuState(rx.State):
    ...
    def check_winner(self):
        winning_combinations = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8],  # 横
            [0, 3, 6], [1, 4, 7], [2, 5, 8],  # 縦
            [0, 4, 8], [2, 4, 6]             # 斜め
        ]
        for combo in winning_combinations:
            if self.board[combo[0]] == self.board[combo[1]] == self.board[combo[2]] != "":
                return True
        return False
    ...
```

##### reset_game

ゲームをリセットする関数です．

```python
class MarubatsuState(rx.State):
    ...
    def reset_game(self):
        self.board = [""] * 9
        self.current_player = PLAYER_A
        self.winner = ""
        self.draw = False
        self.board_colors = [DEFAULT_COLOR] * 9
```

#### 描画用の関数を定義（画面を描画する部分）

`Reflex`のコンポーネントを返す関数を定義します．

コンポーネントの中にコンポーネントを配置することで，複雑な画面を作成することができます．
`rx.cond`を使用することで条件によって表示するコンポーネントを変更することもできます．

```python
def index():
    return rx.center(
        rx.vstack(
            rx.heading("マルバツゲーム", font_size="2em", color=DEFAULT_COLOR),
            rx.grid(
                *[
                    rx.button(
                        MarubatsuState.board[i],
                        on_click=lambda i=i: MarubatsuState.make_move(i),
                        width="60px",
                        height="60px",
                        font_size="2em",
                        background_color=MarubatsuState.board_colors[i]
                    )
                    for i in range(9)
                ],
                grid_template_columns="repeat(3, 1fr)",
                gap="10px",
            ),

            rx.cond(
                MarubatsuState.winner != "",
                rx.text(f"{MarubatsuState.winner}の勝ち", font_size="2em", color=rx.cond(MarubatsuState.winner == PLAYER_A, COLOR_A, COLOR_B)),
                rx.cond(
                    MarubatsuState.draw,
                    rx.text("引き分けです！", font_size="2em"),
                    rx.text(f"{MarubatsuState.current_player}の番です", font_size="2em", color=rx.cond(MarubatsuState.current_player == PLAYER_A, COLOR_A, COLOR_B)),
                ),
            ),
            rx.button("リセット", on_click=MarubatsuState.reset_game, background_color=DEFAULT_COLOR),
            spacing="20px",
        ),
    padding_top="50px",
    ),
```

#### アプリケーションの作成

以下のコードで作成した関数をアプリケーションに追加します．

```python
app = rx.App()
app.add_page(index)
```

#### アプリケーションの実行

最後に以下のコードでアプリケーションを実行します．

```bash
reflex run
```

上記のコマンドを実行後， <http://localhost:3000> にアクセスし，
マルバツゲームが表示されれば成功です．

![マルバツゲームの画面](/images/enken-python-reflex-marubastsu-game/img2.png)

## まとめ

今回は`Reflex`というライブラリを使用するお試しとして，「マルバツゲーム」を作成しました．

Pythonコードだけで簡単にWebアプリを作成できるところが魅力的だと感じました！

## 参考

- [Reflexのドキュメント](https://reflex.dev/)
