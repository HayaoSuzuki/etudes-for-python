---
title: "074: 「注文明細は自分で合計する」の解答"
description: "dataclassとfield(default_factory=...)で注文明細を実装する。"
difficulty: 3
---

# 074: 「注文明細は自分で合計する」の解答

[問題](../problems/074-dataclass-order-line.md) / [ヒント](../hints/074-dataclass-order-line.md)

**難易度:** ☆☆☆

## 方針

`OrderLine` は値を保持する小さなクラスなので、`dataclass` が合います。
ただし、`tags` はリストです。
省略時の値に同じリストを使い回さないように、`field(default_factory=list)` でインスタンスごとに新しいリストを作ります。

## 実装

```python
from dataclasses import dataclass, field


@dataclass
class OrderLine:
    name: str
    unit_price: int
    quantity: int = 1
    tags: list[str] = field(default_factory=list)

    @property
    def subtotal(self):
        return self.unit_price * self.quantity

    def add_tag(self, tag):
        self.tags.append(tag)


def summarize_order(lines):
    return {
        "count": sum(line.quantity for line in lines),
        "total": sum(line.subtotal for line in lines),
        "items": [line.name for line in lines],
    }
```

## 確認

```python
pen = OrderLine("pen", 120, 2)
notebook = OrderLine("notebook", 300)
pen.add_tag("stationery")

assert notebook.tags == []
assert pen.subtotal == 240
assert summarize_order([pen, notebook]) == {
    "count": 3,
    "total": 540,
    "items": ["pen", "notebook"],
}
```

## 発展

検査を加えるなら、`__post_init__` を使うと初期化後に値を確認できます。
あとから属性を書き換える場合まで検査したいなら、プロパティやデスクリプタを使う設計に変わります。

## 参考

- [dataclasses](https://docs.python.org/ja/3.14/library/dataclasses.html)
