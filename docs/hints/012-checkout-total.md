---
title: "012: 「税込み価格は二度ベルを鳴らす」のヒント"
description: "商品価格と個数から小計、税額、合計を整数で求める。"
difficulty: 2
---

# 012: 「税込み価格は二度ベルを鳴らす」のヒント

[問題](../problems/012-checkout-total.md) / [解答](../solutions/012-checkout-total.md)

**難易度:** ☆☆

??? tip "ヒント1"

    `items` を `for price, quantity in items:` で順に取り出せます。

??? tip "ヒント2"

    小計には、各商品の `price * quantity` を足していきます。

??? tip "ヒント3"

    整数の切り捨て除算は `//` です。税額は `subtotal * tax_rate // 100` で求められます。
