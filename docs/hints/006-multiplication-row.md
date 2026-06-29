---
title: "006: 「九つの積の物語」のヒント"
description: "range()とリストを使って、九九の一行を作る。"
difficulty: 1
---

# 006: 「九つの積の物語」のヒント

[問題](../problems/006-multiplication-row.md) / [解答](../solutions/006-multiplication-row.md)

**難易度:** ☆

??? tip "ヒント1"

    `range(1, 10)` は1から9までの整数を順に作ります。

??? tip "ヒント2"

    空のリストを作り、計算結果を `append()` で追加できます。

??? tip "ヒント3"

    `for i in range(1, 10):` の中で `n * i` を計算します。
