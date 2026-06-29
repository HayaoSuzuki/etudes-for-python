---
title: "076: 売上はカンマで区切られる"
description: "csv.DictReaderで売上CSVを読み、商品別と日別に集計する。"
difficulty: 3
---

# 076: 売上はカンマで区切られる

[ヒント](../hints/076-csv-sales-summary.md) / [解答](../solutions/076-csv-sales-summary.md)

**難易度:** ☆☆☆

## 問題

関数 `summarize_sales(csv_text)` を書いてください。

この関数は、売上CSVの文字列を読み、商品別の売上金額と日別の売上金額を集計します。

CSVには、次の列があります。

- `date`
- `item`
- `quantity`
- `unit_price`

## 制約

- `csv.DictReader` を使ってください。
- CSV文字列の1行目はヘッダーです。
- `quantity` と `unit_price` は10進整数として扱います。
- 1行の売上金額は `quantity * unit_price` です。
- `quantity` または `unit_price` が負の場合は `ValueError` を送出してください。
- 必要な列がない場合は `ValueError` を送出してください。
- 戻り値は、キー `by_item` と `by_date` を持つ辞書にしてください。

## 例

```python
>>> text = """date,item,quantity,unit_price
... 2026-06-01,pen,2,120
... 2026-06-01,notebook,1,300
... 2026-06-02,pen,3,120
... """
>>> summarize_sales(text)
{'by_item': {'pen': 600, 'notebook': 300}, 'by_date': {'2026-06-01': 540, '2026-06-02': 360}}
```

## 発展

商品別の数量もあわせて集計してください。

## 参考

- [csv](https://docs.python.org/ja/3.14/library/csv.html)
