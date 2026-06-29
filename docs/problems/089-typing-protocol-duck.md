---
title: "089: 型はふるまいを見ている"
description: "typing.Protocolでrenderメソッドを持つ値を受け取る関数を型付けする。"
difficulty: 4
---

# 089: 型はふるまいを見ている

[ヒント](../hints/089-typing-protocol-duck.md) / [解答](../solutions/089-typing-protocol-duck.md)

**難易度:** ☆☆☆☆

## 問題

`Renderable`、`render_all(items)`、`is_renderable(value)` を書いてください。

`Renderable` は、`render()` メソッドを持つ値を表すプロトコルです。
`render_all` は、渡された値を順に描画用文字列へ変換します。
`is_renderable` は、値が実行時にも `Renderable` とみなせるかを返します。

## 制約

- `typing.Protocol` を使ってください。
- `Renderable` は `render(self) -> str` を持つプロトコルにしてください。
- `isinstance(value, Renderable)` が使えるようにしてください。
- `render_all(items)` は、各要素の `render()` の戻り値をリストで返してください。
- `render_all` の引数と戻り値に型ヒントを付けてください。
- 継承関係に依存せず、同じメソッドを持つ値を受け入れてください。

## 例

```python
>>> class Button:
...     def __init__(self, text):
...         self.text = text
...     def render(self):
...         return f"<button>{self.text}</button>"
...
>>> class Label:
...     def __init__(self, text):
...         self.text = text
...     def render(self):
...         return f"<label>{self.text}</label>"
...
>>> render_all([Button("OK"), Label("Name")])
['<button>OK</button>', '<label>Name</label>']
>>> is_renderable(Button("OK"))
True
>>> is_renderable("plain text")
False
```

## 発展

`render()` が文字列以外を返した場合に、実行時にも検査する関数を追加してください。

## 参考

- [typing](https://docs.python.org/ja/3.14/library/typing.html)
