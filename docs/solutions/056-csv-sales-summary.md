---
title: "056: 「売上はカンマで区切られる」の解答"
description: "csv.DictReaderで行を辞書として読み、売上金額を辞書へ足し込む。"
difficulty: 3
---

# 056: 「売上はカンマで区切られる」の解答

[問題](../problems/056-csv-sales-summary.md) / [ヒント](../hints/056-csv-sales-summary.md)

**難易度:** ☆☆☆

## 方針

CSV文字列は `StringIO` でファイルのようなオブジェクトにし、`csv.DictReader` に渡します。
ヘッダーを確認したあと、各行の数量と単価を整数へ変換します。

1行の売上金額を求めたら、商品別の辞書と日別の辞書へ足し込みます。

## 実装

```python
import csv
from io import StringIO


REQUIRED_COLUMNS = {"date", "item", "quantity", "unit_price"}


def summarize_sales(csv_text):
    reader = csv.DictReader(StringIO(csv_text))

    if reader.fieldnames is None or not REQUIRED_COLUMNS <= set(reader.fieldnames):
        raise ValueError("missing columns")

    by_item = {}
    by_date = {}

    for row in reader:
        quantity = int(row["quantity"])
        unit_price = int(row["unit_price"])
        if quantity < 0 or unit_price < 0:
            raise ValueError("quantity and unit_price must be non-negative")

        amount = quantity * unit_price
        item = row["item"]
        date = row["date"]

        by_item[item] = by_item.get(item, 0) + amount
        by_date[date] = by_date.get(date, 0) + amount

    return {
        "by_item": by_item,
        "by_date": by_date,
    }
```

## 確認

```python
text = """date,item,quantity,unit_price
2026-06-01,pen,2,120
2026-06-01,notebook,1,300
2026-06-02,pen,3,120
"""

assert summarize_sales(text) == {
    "by_item": {"pen": 600, "notebook": 300},
    "by_date": {"2026-06-01": 540, "2026-06-02": 360},
}

try:
    summarize_sales("date,item,quantity,unit_price\n2026-06-01,pen,-1,120\n")
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

`by_item` の値を金額だけでなく、数量と金額を持つ辞書にすると、より実際の集計に近づきます。

## 参考

- [csv](https://docs.python.org/ja/3.14/library/csv.html)

