---
title: "028: 「最大値を探す小さな計算機」のヒント"
description: "SSCアセンブリで2つの入力の最大値を求める。"
difficulty: 3
---

# 028: 「最大値を探す小さな計算機」のヒント

[問題](../problems/028-ssc-maximum-program.md) / [解答](../solutions/028-ssc-maximum-program.md)

**難易度:** ☆☆☆
??? tip "ヒント1"

    `Sub b` のあと、Accumulatorが正なら `a > b` です。

??? tip "ヒント2"

    `a <= b` の場合は、`b` を答えの番地に保存します。

??? tip "ヒント3"

    その後で `a` 側の処理を飛ばすには、Accumulatorに正の定数を読み込んで `Jump output` を実行します。

