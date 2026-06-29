---
title: "057: 小数の請求書は浮かせない"
description: "decimal.Decimalで金額を計算し、税額を小数第2位へ丸める。"
difficulty: 3
---

# 057: 小数の請求書は浮かせない

[ヒント](../hints/057-decimal-invoice-total.md) / [解答](../solutions/057-decimal-invoice-total.md)

**難易度:** ☆☆☆

## 問題

関数 `invoice_total(items, tax_rate)` を書いてください。

`items` は、商品名、単価、数量のタプルのリストです。
単価と税率は10進小数の文字列で渡されます。
小計、税額、合計を `Decimal` で返してください。

## 制約

- `decimal.Decimal` を使ってください。
- 単価と税率を `float` に変換してはいけません。
- `items` の各要素は `(name, unit_price, quantity)` です。
- `unit_price` は文字列、`quantity` は整数です。
- 税額は、`ROUND_HALF_UP` で小数第2位までに丸めてください。
- 戻り値は、キー `subtotal`、`tax`、`total` を持つ辞書です。
- 3つの値はすべて、小数第2位までの `Decimal` にしてください。

## 例

```python
>>> from decimal import Decimal
>>> invoice_total([("pen", "120.00", 2), ("notebook", "250.00", 1)], "0.10")
{'subtotal': Decimal('490.00'), 'tax': Decimal('49.00'), 'total': Decimal('539.00')}
>>> invoice_total([("fee", "0.05", 1)], "0.10")
{'subtotal': Decimal('0.05'), 'tax': Decimal('0.01'), 'total': Decimal('0.06')}
```

## 発展

商品ごとの割引率を追加してください。

## 参考

- [decimal](https://docs.python.org/ja/3.14/library/decimal.html)

