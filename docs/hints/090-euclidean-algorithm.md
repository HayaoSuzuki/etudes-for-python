---
title: "090: 「G.C.D」のヒント"
description: "余りを使って問題を小さくする。"
difficulty: 2
---

# 090: 「G.C.D」のヒント

[問題](../problems/090-euclidean-algorithm.md) / [解答](../solutions/090-euclidean-algorithm.md)

**難易度:** ☆☆

??? tip "ヒント1"

    Euclidの互除法では、`gcd(a, b)` と `gcd(b, a % b)` が同じ値になることを使います。

??? tip "ヒント2"

    `a % b` は、`a` を `b` で割った余りです。
    余りが0になったとき、そのときの割る数が最大公約数です。

??? tip "ヒント3"

    `while b != 0:` の間、`a, b = b, a % b` と更新します。
    ループが止まったときの `a` が答えです。

??? tip "ヒント4"

    `gcd(0, b)` は `b` です。
    この場合も、同じループで処理できます。

