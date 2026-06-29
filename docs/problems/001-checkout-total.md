---
title: "001: レジは明細を覚えている"
description: "商品表と買い物かごから、明細、小計、税額、合計、おつりをまとめたレシートを作る。"
difficulty: 1
---

# 001: レジは明細を覚えている

[ヒント](../hints/001-checkout-total.md) / [解答](../solutions/001-checkout-total.md)

**難易度:** ☆
## 問題

関数 `checkout_receipt(catalog, cart, tax_rate, paid)` を書いてください。
この関数は、商品表 `catalog`、買い物かご `cart`、税率 `tax_rate`、支払額 `paid` を受け取り、レシートを表す辞書を返します。

`catalog` は商品コードをキー、税抜き単価を値にする辞書です。
`cart` は `(code, quantity)` のタプルのリストです。
同じ商品コードが複数回出てくることがあります。

戻り値の辞書は、次のキーを持ちます。

- `"lines"`：`(code, quantity, line_total)` のリスト
- `"subtotal"`：税抜き小計
- `"tax"`：税額
- `"total"`：税込み合計
- `"change"`：おつり

`"lines"` では、同じ商品コードをまとめてください。
商品の順番は、`cart` に初めて出てきた順にします。

## 制約

- 単価、個数、税率、支払額は0以上の整数です。
- 税額は、小計全体に税率をかけ、小数点以下を切り捨てます。
- `cart` に `catalog` にない商品コードが出た場合は `KeyError` を送出してください。
- 支払額が税込み合計に足りない場合は `ValueError` を送出してください。
- `cart` は空でもかまいません。

## 例

```python
>>> catalog = {"tea": 120, "cake": 300, "bag": 5}
>>> cart = [("tea", 2), ("cake", 1), ("tea", 1)]
>>> checkout_receipt(catalog, cart, 10, 1000)
{'lines': [('tea', 3, 360), ('cake', 1, 300)], 'subtotal': 660, 'tax': 66, 'total': 726, 'change': 274}
>>> checkout_receipt(catalog, [], 10, 0)
{'lines': [], 'subtotal': 0, 'tax': 0, 'total': 0, 'change': 0}
>>> checkout_receipt(catalog, [("tea", 1)], 10, 100)
Traceback (most recent call last):
...
ValueError: paid amount is not enough
```

## 発展

数量が0の商品を明細から取り除く版を書いてください。