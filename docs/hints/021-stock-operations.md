---
title: "021: 「在庫は夜に減っている」のヒント"
description: "在庫辞書に入出庫操作を適用し、負の在庫を拒否する。"
difficulty: 4
---

# 021: 「在庫は夜に減っている」のヒント

[問題](../problems/021-stock-operations.md) / [解答](../solutions/021-stock-operations.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    元の辞書を変えないために、まずコピーを作ります。

??? tip "ヒント2"

    辞書にない商品の在庫は、`get(name, 0)` で0として取り出せます。

??? tip "ヒント3"

    変更後の在庫が負になったら、そこで `ValueError` を送出します。
