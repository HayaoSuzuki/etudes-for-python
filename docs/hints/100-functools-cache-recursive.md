---
title: "100: 「道順は覚えて数える」のヒント"
description: "functools.cacheで再帰的な格子経路数の重複計算を避ける。"
difficulty: 4
---

# 100: 「道順は覚えて数える」のヒント

[問題](../problems/100-functools-cache-recursive.md) / [解答](../solutions/100-functools-cache-recursive.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    最後の1歩に注目します。
    右から来た場合と上から来た場合の2通りに分けられます。

??? tip "ヒント2"

    `count_paths(width, height)` は、`count_paths(width - 1, height)` と `count_paths(width, height - 1)` の和で表せます。

??? tip "ヒント3"

    `width == 0` または `height == 0` のときは、まっすぐ進む1通りだけです。

??? tip "ヒント4"

    同じ `(width, height)` を何度も計算しないように、内側の再帰関数へ `@cache` を付けます。
