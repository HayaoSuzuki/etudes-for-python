---
title: "065: 「メモリの中だけの売上表」の解答"
description: "sqlite3のインメモリDBに行を挿入し、GROUP BYで商品別売上を集計する。"
difficulty: 4
---

# 065: 「メモリの中だけの売上表」の解答

[問題](../problems/065-sqlite-memory-report.md) / [ヒント](../hints/065-sqlite-memory-report.md)

**難易度:** ☆☆☆☆

## 方針

`:memory:` に接続すると、ファイルを作らずにSQLiteデータベースを使えます。
売上行をテーブルへ入れ、SQLの `GROUP BY` で商品別に集計します。

値をSQL文字列へ直接埋め込まず、プレースホルダで渡します。

## 実装

```python
import sqlite3


def sales_report(rows):
    with sqlite3.connect(":memory:") as connection:
        connection.execute(
            """
            CREATE TABLE sales (
                date TEXT NOT NULL,
                item TEXT NOT NULL,
                quantity INTEGER NOT NULL,
                unit_price INTEGER NOT NULL
            )
            """
        )
        connection.executemany(
            "INSERT INTO sales (date, item, quantity, unit_price) VALUES (?, ?, ?, ?)",
            rows,
        )
        cursor = connection.execute(
            """
            SELECT item, SUM(quantity * unit_price) AS total
            FROM sales
            GROUP BY item
            ORDER BY total DESC, item ASC
            """
        )
        return cursor.fetchall()
```

## 確認

```python
rows = [
    ("2026-06-01", "pen", 2, 120),
    ("2026-06-01", "notebook", 1, 300),
    ("2026-06-02", "pen", 3, 120),
]

assert sales_report(rows) == [("pen", 600), ("notebook", 300)]
```

## 発展

集計対象が大きくなると、日付範囲や商品名で絞り込む条件が必要になります。
その場合も、条件値はプレースホルダで渡します。

## 参考

- [sqlite3](https://docs.python.org/ja/3.14/library/sqlite3.html)

