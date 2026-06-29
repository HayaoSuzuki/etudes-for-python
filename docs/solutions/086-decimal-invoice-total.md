---
title: "086: 「小数の請求書は浮かせない」の解答"
description: "Decimalとquantizeで金額と税額を小数第2位にそろえる。"
difficulty: 3
---

# 086: 「小数の請求書は浮かせない」の解答

[問題](../problems/086-decimal-invoice-total.md) / [ヒント](../hints/086-decimal-invoice-total.md)

**難易度:** ☆☆☆

## 方針

単価と税率は文字列から `Decimal` に変換します。
`float` を経由すると、10進小数として期待した値とずれることがあります。

小数第2位までにそろえるため、`Decimal("0.01")` を使って `quantize` します。
丸め方法は `ROUND_HALF_UP` を指定します。

## 実装

```python
from decimal import Decimal, ROUND_HALF_UP


CENT = Decimal("0.01")


def money(value):
    return value.quantize(CENT, rounding=ROUND_HALF_UP)


def invoice_total(items, tax_rate):
    subtotal = sum(
        Decimal(unit_price) * quantity
        for _, unit_price, quantity in items
    )
    subtotal = money(subtotal)
    tax = money(subtotal * Decimal(tax_rate))
    total = money(subtotal + tax)

    return {
        "subtotal": subtotal,
        "tax": tax,
        "total": total,
    }
```

## 確認

```python
assert invoice_total([("pen", "120.00", 2), ("notebook", "250.00", 1)], "0.10") == {
    "subtotal": Decimal("490.00"),
    "tax": Decimal("49.00"),
    "total": Decimal("539.00"),
}

assert invoice_total([("fee", "0.05", 1)], "0.10") == {
    "subtotal": Decimal("0.05"),
    "tax": Decimal("0.01"),
    "total": Decimal("0.06"),
}
```

## 発展

商品ごとに税率が違う場合は、行ごとに税額を丸めるのか、小計を合算してから税額を丸めるのかで結果が変わることがあります。
請求書では、どの段階で丸めるかも仕様として決める必要があります。

## 参考

- [decimal](https://docs.python.org/ja/3.14/library/decimal.html)
