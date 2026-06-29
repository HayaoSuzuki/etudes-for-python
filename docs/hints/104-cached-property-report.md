---
title: "104: 「重い集計は一度だけ」のヒント"
description: "functools.cached_propertyで集計結果をインスタンスにキャッシュする。"
difficulty: 4
---

# 104: 「重い集計は一度だけ」のヒント

[問題](../problems/104-cached-property-report.md) / [解答](../solutions/104-cached-property-report.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `cached_property` は、初回アクセス時にメソッドを実行し、その結果をインスタンスに保存します。
    2回目以降は保存された値が返ります。

??? tip "ヒント2"

    計算回数を数えるため、インスタンスに `_build_count` を持たせます。
    `totals_by_item` の中で1増やします。

??? tip "ヒント3"

    商品別合計は、辞書に `amount` を足し込んで作ります。

??? tip "ヒント4"

    `top_item` は `totals_by_item` を使って求めます。
    同額の場合の結果を安定させるなら、合計の降順、商品名の昇順で並べます。
