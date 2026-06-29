---
title: "057: 「小数の請求書は浮かせない」のヒント"
description: "decimal.Decimalで金額を計算し、税額を小数第2位へ丸める。"
difficulty: 3
---

# 057: 「小数の請求書は浮かせない」のヒント

[問題](../problems/057-decimal-invoice-total.md) / [解答](../solutions/057-decimal-invoice-total.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    金額を2進浮動小数点数で扱うと、10進小数を正確に表せないことがあります。
    今回は文字列から `Decimal` を作ります。

??? tip "ヒント2"

    小数第2位までにそろえるには、`Decimal("0.01")` を使って `quantize` します。

??? tip "ヒント3"

    四捨五入の種類は `rounding` 引数で指定できます。
    今回は `ROUND_HALF_UP` を使います。

??? tip "ヒント4"

    小計は商品ごとの `Decimal(unit_price) * quantity` の合計です。
    税額を丸め、最後に小計と税額を足して合計も同じ桁にそろえます。

