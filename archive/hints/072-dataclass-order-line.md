---
title: "072: 「注文明細は自分で合計する」のヒント"
description: "dataclassで注文明細を表し、default_factoryでインスタンスごとのリストを持つ。"
difficulty: 3
---

# 072: 「注文明細は自分で合計する」のヒント

[問題](../problems/072-dataclass-order-line.md) / [解答](../solutions/072-dataclass-order-line.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `@dataclass` を付けると、`__init__` や表示用のメソッドを自分で書かなくても、フィールドから自動で作られます。

??? tip "ヒント2"

    リストを省略時の値にしたい場合、`tags=[]` のようには書きません。
    インスタンスごとに新しいリストを作る必要があります。

??? tip "ヒント3"

    `field(default_factory=list)` を使うと、`OrderLine` を作るたびに別々の空リストを用意できます。

??? tip "ヒント4"

    `subtotal` は属性のように読める値なので、メソッドではなく `@property` にすると使いやすくなります。
    集計関数では、各行の `quantity`、`subtotal`、`name` を順に集めます。

