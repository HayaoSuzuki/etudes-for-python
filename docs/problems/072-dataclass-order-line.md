---
title: "072: 注文明細は自分で合計する"
description: "dataclassで注文明細を表し、default_factoryでインスタンスごとのリストを持つ。"
difficulty: 3
---

# 072: 注文明細は自分で合計する

[ヒント](../hints/072-dataclass-order-line.md) / [解答](../solutions/072-dataclass-order-line.md)

**難易度:** ☆☆☆

## 問題

`OrderLine` と `summarize_order(lines)` を書いてください。

`OrderLine` は、商品名、単価、数量、タグを持つ注文明細です。
単価と数量から小計を求められるようにしてください。

`summarize_order(lines)` は、注文明細のリストを受け取り、合計数量、合計金額、商品名のリストを辞書で返します。

## 制約

- `OrderLine` は `dataclasses.dataclass` を使って定義してください。
- `OrderLine` は `name`、`unit_price`、`quantity`、`tags` を持ちます。
- `quantity` の省略時の値は `1` とします。
- `tags` の省略時の値は空のリストとします。
- `tags` はインスタンスごとに別々のリストにしてください。
- `OrderLine.subtotal` は、単価と数量を掛けた値を返すプロパティにしてください。
- `OrderLine.add_tag(tag)` は、タグを追加して `None` を返します。
- `summarize_order(lines)` は、キー `count`、`total`、`items` を持つ辞書を返します。

## 例

```python
>>> pen = OrderLine("pen", 120, 2)
>>> notebook = OrderLine("notebook", 300)
>>> pen.add_tag("stationery")
>>> notebook.tags
[]
>>> pen.subtotal
240
>>> summarize_order([pen, notebook])
{'count': 3, 'total': 540, 'items': ['pen', 'notebook']}
```

## 発展

数量や単価に負の値が入らないように検査してください。

## 参考

- [dataclasses](https://docs.python.org/ja/3.14/library/dataclasses.html)

