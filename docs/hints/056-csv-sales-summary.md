---
title: "056: 「売上はカンマで区切られる」のヒント"
description: "csv.DictReaderで売上CSVを読み、商品別と日別に集計する。"
difficulty: 3
---

# 056: 「売上はカンマで区切られる」のヒント

[問題](../problems/056-csv-sales-summary.md) / [解答](../solutions/056-csv-sales-summary.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `csv.DictReader` は、1行目のヘッダーを使って各行を辞書として返します。
    文字列をファイルのように読むには `io.StringIO` が使えます。

??? tip "ヒント2"

    `reader.fieldnames` を見ると、CSVに含まれる列名を確認できます。
    必要な列の集合がすべて含まれているかを先に検査します。

??? tip "ヒント3"

    `quantity` と `unit_price` は文字列として読まれます。
    集計する前に `int()` で整数へ変換します。

??? tip "ヒント4"

    1行ごとに `quantity * unit_price` を計算し、商品名の辞書と日付の辞書へそれぞれ足し込みます。
    まだないキーは0から始めます。

