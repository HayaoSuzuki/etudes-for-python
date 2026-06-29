---
title: "001: 「レジは明細を覚えている」の解答"
description: "商品コードごとの数量を集計し、明細と合計を順に作る。"
difficulty: 1
---

# 001: 「レジは明細を覚えている」の解答

[問題](../problems/001-checkout-total.md) / [ヒント](../hints/001-checkout-total.md)

**難易度:** ☆
## 方針

買い物かごをそのまま合計すると、同じ商品が複数行に分かれます。
先に商品コードごとの数量を辞書に集計します。

ただし、レシートの明細順は入力順です。
そのため、数量の辞書とは別に、商品コードが初めて出た順番をリストで持ちます。

## 実装

```python
def checkout_receipt(catalog, cart, tax_rate, paid):
    quantities = {}
    order = []

    for code, quantity in cart:
        if code not in catalog:
            raise KeyError(code)
        if code not in quantities:
            quantities[code] = 0
            order.append(code)
        quantities[code] += quantity

    lines = []
    subtotal = 0
    for code in order:
        quantity = quantities[code]
        line_total = catalog[code] * quantity
        lines.append((code, quantity, line_total))
        subtotal += line_total

    tax = subtotal * tax_rate // 100
    total = subtotal + tax
    if paid < total:
        raise ValueError("paid amount is not enough")

    return {
        "lines": lines,
        "subtotal": subtotal,
        "tax": tax,
        "total": total,
        "change": paid - total,
    }
```

## 確認

```python
catalog = {"tea": 120, "cake": 300, "bag": 5}
cart = [("tea", 2), ("cake", 1), ("tea", 1)]
assert checkout_receipt(catalog, cart, 10, 1000) == {
    "lines": [("tea", 3, 360), ("cake", 1, 300)],
    "subtotal": 660,
    "tax": 66,
    "total": 726,
    "change": 274,
}
assert checkout_receipt(catalog, [], 10, 0) == {
    "lines": [],
    "subtotal": 0,
    "tax": 0,
    "total": 0,
    "change": 0,
}

try:
    checkout_receipt(catalog, [("tea", 1)], 10, 100)
except ValueError as exc:
    assert str(exc) == "paid amount is not enough"
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

数量が0の商品を消す場合は、明細を作るループで `quantity == 0` の行を飛ばします。
ただし、負の数量を返品として扱うなら、小計や支払額の意味も決め直す必要があります。