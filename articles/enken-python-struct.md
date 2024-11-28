---
title: "Pythonで構造体みたいなデータを扱いたいときに標準で使える候補"
emoji: "⚓️"
type: "tech"
topics: ["python"]
published: true
---

## はじめに

Pythonで型を意識しつつ，構造体のようなデータを扱いたいときに，標準で使える候補として以下の3つがあります．

- `dataclasses`
- `NamedTuple`
- `TypedDict`

それぞれ使い方と簡単な特徴を紹介します．

## dataclasses

`dataclasses`は以下のように使います．

```python
from dataclasses import dataclass

@dataclass
class MyStruct:
    id: int
    name: str
    active: bool

# 使用例
data = MyStruct(id=1, name="Test", active=True)
print(data) # MyStruct(id=1, name='Test', active=True)

# idの値を変更する
data.id = 2
print(data) # MyStruct(id=2, name='Test', active=True)

# idの値をstr型で変更する
data.id = "a"
print(data) # MyStruct(id='a', name='Test', active=True)
# エラーになりません

# 新しい属性を追加してみる
data.description = "説明"
print(data) # MyStruct(id='a', name='Test', active=True)
print(data.description) # 説明
# 追加されます

# 比較が可能です
data2 = MyStruct(id="a", name="Test", active=True)
print(data == data2) # True

@dataclass
class OtherStruct:
    id: int
    name: str
    active: bool

# 構造が同じでも，クラスが異なれば比較はFalseになります
data3 = OtherStruct(id="a", name="Test", active=True)
print(data == data3) # False

# イミュータブルにすることもできます
@dataclass(frozen=True)
class MyImmutableStruct:
    id: int
    name: str
    active: bool

# インスタンス作成
data = MyImmutableStruct(id=1, name="Test", active=True)
print(data)  # MyImmutableStruct(id=1, name='Test', active=True)

# 属性を変更しようとするとエラーになります
# data.id = 2  # dataclasses.FrozenInstanceError: cannot assign to field 'id'
```

簡単な特徴

- イミュータブルにもできる．
- パラメータでいろいろ指定できる．

## NamedTuple

`NamedTuple`は以下のように使います．

```python
from typing import NamedTuple

class MyStruct(NamedTuple):
    id: int
    name: str
    active: bool

data = MyStruct(id=1, name="Test", active=True)
print(data) # MyStruct(id=1, name='Test', active=True)

# 値を変更しようとするとエラーになります
# data.id = 2 # AttributeError: can't set attribute

data2 = MyStruct(id=1, active=True, name="Test") # #順番を変えてもOK
print(data2) # MyStruct(id=1, name='Test', active=False)

# 普通のタプルと比較も可能です．
data3 = (1, "Test", True)
print(data == data2) # True
print(data == data3) # True

# それぞれに取り出すことができます
id, name, active = data
print(name) # Test

# 順番が重要です
id, active, name = data
print(name) # True 
```

気を付けるべき使用例としては，以下のようなものがあります．

```python

class News(NamedTuple):
    north: str
    east: str
    west: str
    south: str

class EastNorth(NamedTuple):
    east: str
    north: str

en = EastNorth(east="東", north="北")
print(en) # EastNorth(east='東', north='北') 
news = News(*en, west="西", south="南")
print(news) # News(north='東', east='北', west='西', south='南')
# northとeastが逆になってしまう
```

Namedですが，それを用いてうまく代入されるわけではないです．

簡単な特徴

- `NamedTuple`は後から値を変更できない．
- タプルとして等しければ，それらは等しいと判定される．

## TypedDict

`TypedDict`は以下のように使います．

```python
from typing import TypedDict

class MyStruct(TypedDict):
    id: int
    name: str
    active: bool

# 使用例
data: MyStruct = {"id": 1, "name": "Test", "active": True}
print(data) # {'id': 1, 'name': 'Test', 'active': True}

# .(ドット)でアクセスはできない
# data.id = 2 #'dict' object has no attribute 'id'

# 辞書のように更新できる
data["id"] = 2
print(data) # {'id': 2, 'name': 'Test', 'active': True}

# インデックスではなく，keyとなる．
data[0] = 3
print(data) # {'id': 2, 'name': 'Test', 'active': True, 0: 3}

# 辞書と比較が可能
data2 = {'id': 2, 'name': 'Test', 'active': True, 0: 3}
print(data == data2) # True

# タイプはdict
print(type(data)) # <class 'dict'>
print(type({"a": 1})) # <class 'dict'>
```

簡単な特徴

- `TypedDict`は辞書として扱われる．

## まとめ

どれでも良いなら，`dataclasses`を使うかな，というところです．
