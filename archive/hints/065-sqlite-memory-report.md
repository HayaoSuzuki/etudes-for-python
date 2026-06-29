---
title: "065: 「メモリの中だけの売上表」のヒント"
description: "sqlite3のインメモリDBに売上を入れ、集計クエリで商品別売上を返す。"
difficulty: 4
---

# 065: 「メモリの中だけの売上表」のヒント

[問題](../problems/065-sqlite-memory-report.md) / [解答](../solutions/065-sqlite-memory-report.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `sqlite3.connect(":memory:")` で、ファイルを作らない一時的なデータベースを使えます。

??? tip "ヒント2"

    まず `CREATE TABLE` で列を定義し、`INSERT INTO` で `rows` の内容を入れます。
    値はSQL文字列へ直接埋め込まず、`?` のプレースホルダで渡します。

??? tip "ヒント3"

    商品別に集計するには、`GROUP BY item` を使います。
    合計金額は `SUM(quantity * unit_price)` で求められます。

??? tip "ヒント4"

    並び順はSQL側で指定できます。
    `ORDER BY total DESC, item ASC` のように、集計結果に名前を付けてから並べます。

