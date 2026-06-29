---
title: "087: メモリの中だけの売上表"
description: "sqlite3のインメモリDBに売上を入れ、集計クエリで商品別売上を返す。"
difficulty: 4
---

# 087: メモリの中だけの売上表

[ヒント](../hints/087-sqlite-memory-report.md) / [解答](../solutions/087-sqlite-memory-report.md)

**難易度:** ☆☆☆☆

## 問題

関数 `sales_report(rows)` を書いてください。

この関数は、売上行をSQLiteのインメモリDBに入れ、商品別の売上金額を集計します。

## 制約

- `sqlite3` を使ってください。
- データベースは `:memory:` に作ってください。
- `rows` の各要素は `(date, item, quantity, unit_price)` のタプルです。
- `quantity` と `unit_price` は整数です。
- 売上金額は `quantity * unit_price` です。
- SQLへの値の受け渡しにはプレースホルダを使ってください。
- 戻り値は `(item, total)` のタプルのリストです。
- 合計金額の降順、同額なら商品名の昇順で並べてください。

## 例

```python
>>> rows = [
...     ("2026-06-01", "pen", 2, 120),
...     ("2026-06-01", "notebook", 1, 300),
...     ("2026-06-02", "pen", 3, 120),
... ]
>>> sales_report(rows)
[('pen', 600), ('notebook', 300)]
```

## 発展

日付ごとの集計も返すようにしてください。

## 参考

- [sqlite3](https://docs.python.org/ja/3.14/library/sqlite3.html)
