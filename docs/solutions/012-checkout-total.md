---
title: "012: 「税込み価格は二度ベルを鳴らす」の解答"
description: "商品価格と個数から小計、税額、合計を整数で求める。"
difficulty: 2
---

# 012: 「税込み価格は二度ベルを鳴らす」の解答

[問題](../problems/012-checkout-total.md) / [ヒント](../hints/012-checkout-total.md)

**難易度:** ☆☆

## 方針

まず、商品ごとの金額を合計して小計を作ります。
その小計に税率をかけ、100で割った整数部分を税額にします。
最後に、小計と税額を足して合計を求めます。

## 実装

```python
def checkout_total(items, tax_rate):
    subtotal = 0
    for price, quantity in items:
        subtotal += price * quantity

    tax = subtotal * tax_rate // 100
    total = subtotal + tax
    return (subtotal, tax, total)
```

## 確認

```python
assert checkout_total([(120, 2), (80, 3)], 10) == (480, 48, 528)
assert checkout_total([(99, 1)], 10) == (99, 9, 108)
assert checkout_total([], 10) == (0, 0, 0)
```

## 発展

商品ごとに税額を切り捨てる場合は、各商品の金額を求めた直後に税額を計算します。
この問題の実装とは端数処理の位置が変わるので、同じ買い物でも合計が変わることがあります。
