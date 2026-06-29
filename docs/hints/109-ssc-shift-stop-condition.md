---
title: "109: 「止まらない二倍の列」のヒント"
description: "Python整数版のShiftループと8ビット符号付き解釈の停止条件を比較する。"
difficulty: 4
---

# 109: 「止まらない二倍の列」のヒント

[問題](../problems/109-ssc-shift-stop-condition.md) / [解答](../solutions/109-ssc-shift-stop-condition.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    Python整数版では、単に `value << 1` を繰り返します。

??? tip "ヒント2"

    8ビット符号付きにするには、まず `value % 256` で下位8ビットだけを残します。

??? tip "ヒント3"

    下位8ビットの値が128以上なら、符号付き整数としては負の値です。

