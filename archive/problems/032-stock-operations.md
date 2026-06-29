---
title: "032: 在庫は夜に減っている"
description: "在庫辞書に入出庫操作を適用し、負の在庫を拒否する。"
difficulty: 4
---

# 032: 在庫は夜に減っている

[ヒント](../hints/032-stock-operations.md) / [解答](../solutions/032-stock-operations.md)

**難易度:** ☆☆☆☆

## 問題

関数 `apply_stock(initial, operations)` を書いてください。
この関数は、最初の在庫数を表す辞書 `initial` と、入出庫操作のリスト `operations` を受け取り、操作後の在庫辞書を返します。

`initial` は、商品名をキー、在庫数を値にする辞書です。
`operations` の各要素は `(name, change)` のタプルで、`change` が正なら入庫、負なら出庫を表します。

操作の途中で在庫が負になる場合は、`ValueError` を送出してください。
元の `initial` は変更しないでください。

## 制約

- 商品名は文字列です。
- 在庫数と `change` は整数です。
- `operations` にだけ出てくる商品は、最初の在庫数を0として扱います。

## 例

```python
>>> apply_stock({"tea": 10, "cake": 2}, [("tea", -3), ("coffee", 5)])
{'tea': 7, 'cake': 2, 'coffee': 5}
>>> initial = {"tea": 1}
>>> updated = apply_stock(initial, [("tea", 2)])
>>> initial
{'tea': 1}
>>> updated
{'tea': 3}
>>> apply_stock({"tea": 1}, [("tea", -2)])
Traceback (most recent call last):
...
ValueError: stock cannot be negative
```

## 発展

在庫が0になった商品を、返す辞書から取り除く版も書いてください。

