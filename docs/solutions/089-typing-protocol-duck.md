---
title: "089: 「型はふるまいを見ている」の解答"
description: "Protocolとruntime_checkableでrenderメソッドを持つ値を型として表す。"
difficulty: 4
---

# 089: 「型はふるまいを見ている」の解答

[問題](../problems/089-typing-protocol-duck.md) / [ヒント](../hints/089-typing-protocol-duck.md)

**難易度:** ☆☆☆☆

## 方針

`Protocol` を使うと、特定の基底クラスを継承していなくても、必要なメソッドを持つ値を型として表せます。
今回は `render() -> str` を持つ値を `Renderable` とします。

実行時に `isinstance(value, Renderable)` を使うため、`@runtime_checkable` を付けます。

## 実装

```python
from collections.abc import Iterable
from typing import Protocol, runtime_checkable


@runtime_checkable
class Renderable(Protocol):
    def render(self) -> str:
        ...


def render_all(items: Iterable[Renderable]) -> list[str]:
    return [item.render() for item in items]


def is_renderable(value) -> bool:
    return isinstance(value, Renderable)
```

## 確認

```python
class Button:
    def __init__(self, text):
        self.text = text

    def render(self):
        return f"<button>{self.text}</button>"


class Label:
    def __init__(self, text):
        self.text = text

    def render(self):
        return f"<label>{self.text}</label>"


assert render_all([Button("OK"), Label("Name")]) == [
    "<button>OK</button>",
    "<label>Name</label>",
]
assert is_renderable(Button("OK")) is True
assert is_renderable("plain text") is False
```

## 発展

`@runtime_checkable` による判定は、メソッドがあるかどうかを見ます。
戻り値の型までは実行時に確認しません。
必要なら、`render()` を実際に呼び出し、戻り値が文字列かどうかを検査する別の関数を用意します。

## 参考

- [typing](https://docs.python.org/ja/3.14/library/typing.html)
