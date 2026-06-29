---
title: "021: 「在庫は夜に減っている」の解答"
description: "在庫辞書に入出庫操作を適用し、負の在庫を拒否する。"
difficulty: 4
---

# 021: 「在庫は夜に減っている」の解答

[問題](../problems/021-stock-operations.md) / [ヒント](../hints/021-stock-operations.md)

**難易度:** ☆☆☆☆

## 方針

まず `initial.copy()` で作業用の辞書を作ります。
各操作では、現在の在庫数に変化量を足します。
足した結果が負ならエラーにし、そうでなければ辞書を更新します。

## 実装

```python
def apply_stock(initial, operations):
    stock = initial.copy()
    for name, change in operations:
        new_count = stock.get(name, 0) + change
        if new_count < 0:
            raise ValueError("stock cannot be negative")
        stock[name] = new_count
    return stock
```

## 確認

```python
assert apply_stock({"tea": 10, "cake": 2}, [("tea", -3), ("coffee", 5)]) == {"tea": 7, "cake": 2, "coffee": 5}
initial = {"tea": 1}
updated = apply_stock(initial, [("tea", 2)])
assert initial == {"tea": 1}
assert updated == {"tea": 3}
try:
    apply_stock({"tea": 1}, [("tea", -2)])
except ValueError as exc:
    assert str(exc) == "stock cannot be negative"
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

在庫0の商品を取り除く場合は、操作をすべて適用したあとで別の辞書を作ると安全です。
ループ中の辞書から要素を削除すると、処理が読みづらくなります。
