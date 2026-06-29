---
title: "092: 「同じ値はまとめて走る」のヒント"
description: "itertools.groupbyで連続する同じ値をランレングス符号化する。"
difficulty: 3
---

# 092: 「同じ値はまとめて走る」のヒント

[問題](../problems/092-itertools-run-length.md) / [解答](../solutions/092-itertools-run-length.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    ランレングス符号化では、同じ値が連続している部分だけをまとめます。
    離れた場所に同じ値があっても、別のまとまりとして扱います。

??? tip "ヒント2"

    `itertools.groupby(items)` は、連続する同じ値ごとに `(key, group)` を返します。
    `group` は、そのまとまりに属する値を順に出すイテレータです。

??? tip "ヒント3"

    各 `group` の長さは、`sum(1 for _ in group)` で数えられます。

??? tip "ヒント4"

    復元では、`value` を `count` 回だけ結果リストに追加します。
    `count <= 0` は不正な入力として先に拒否します。
