---
title: "098: 「点数の分布を読む」のヒント"
description: "statisticsで平均、中央値、母標準偏差を求める。"
difficulty: 3
---

# 098: 「点数の分布を読む」のヒント

[問題](../problems/098-statistics-score-report.md) / [解答](../solutions/098-statistics-score-report.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    空のリストでは平均や中央値を定義できません。
    まず入力が空かどうかを確認します。

??? tip "ヒント2"

    `statistics.mean`、`statistics.median`、`statistics.pstdev` が使えます。
    `pstdev` は母標準偏差です。

??? tip "ヒント3"

    `statistics` の戻り値は、入力によって整数に見えることがあります。
    問題の仕様に合わせて `float(...)` でそろえます。

??? tip "ヒント4"

    辞書の `count` には `len(scores)` を入れます。
    ほかの3つは `statistics` の関数で計算します。
