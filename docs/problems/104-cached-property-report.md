---
title: "104: 重い集計は一度だけ"
description: "functools.cached_propertyで集計結果をインスタンスにキャッシュする。"
difficulty: 4
---

# 104: 重い集計は一度だけ

[ヒント](../hints/104-cached-property-report.md) / [解答](../solutions/104-cached-property-report.md)

**難易度:** ☆☆☆☆

## 問題

クラス `SalesReport` を書いてください。

`SalesReport(records)` は、売上レコードのリストを受け取ります。
商品別売上合計を `totals_by_item` プロパティで返してください。

## 制約

- `functools.cached_property` を使ってください。
- `records` の各要素は、キー `item` と `amount` を持つ辞書です。
- `totals_by_item` は、商品名から合計金額への辞書を返します。
- `totals_by_item` は同じインスタンスでは一度だけ計算してください。
- 計算回数を確認できる読み取り専用プロパティ `build_count` を用意してください。
- `top_item` は、売上合計が最大の商品名を返すプロパティにしてください。

## 例

```python
>>> report = SalesReport([
...     {"item": "pen", "amount": 120},
...     {"item": "notebook", "amount": 300},
...     {"item": "pen", "amount": 180},
... ])
>>> report.totals_by_item
{'pen': 300, 'notebook': 300}
>>> report.totals_by_item is report.totals_by_item
True
>>> report.build_count
1
>>> report.top_item
'notebook'
```

## 発展

レコードを追加したときにキャッシュを破棄するメソッドを追加してください。

## 参考

- [functools.cached_property](https://docs.python.org/ja/3.14/library/functools.html#functools.cached_property)
