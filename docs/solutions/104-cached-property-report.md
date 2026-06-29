---
title: "104: 「重い集計は一度だけ」の解答"
description: "cached_propertyで商品別合計を一度だけ計算し、以後はキャッシュを返す。"
difficulty: 4
---

# 104: 「重い集計は一度だけ」の解答

[問題](../problems/104-cached-property-report.md) / [ヒント](../hints/104-cached-property-report.md)

**難易度:** ☆☆☆☆

## 方針

`totals_by_item` を `cached_property` にします。
初回アクセス時に商品別合計を作り、同じインスタンスではその結果を再利用します。

計算された回数を確認できるように、`_build_count` を更新します。

## 実装

```python
from functools import cached_property


class SalesReport:
    def __init__(self, records):
        self.records = list(records)
        self._build_count = 0

    @cached_property
    def totals_by_item(self):
        self._build_count += 1
        totals = {}
        for record in self.records:
            item = record["item"]
            totals[item] = totals.get(item, 0) + record["amount"]
        return totals

    @property
    def build_count(self):
        return self._build_count

    @property
    def top_item(self):
        if not self.totals_by_item:
            return None
        return sorted(
            self.totals_by_item.items(),
            key=lambda item: (-item[1], item[0]),
        )[0][0]
```

## 確認

```python
report = SalesReport([
    {"item": "pen", "amount": 120},
    {"item": "notebook", "amount": 300},
    {"item": "pen", "amount": 180},
])

assert report.totals_by_item == {"pen": 300, "notebook": 300}
assert report.totals_by_item is report.totals_by_item
assert report.build_count == 1
assert report.top_item == "notebook"
```

## 発展

`cached_property` は、元データが変わっても自動では再計算しません。
データを変更する設計にするなら、キャッシュを削除するタイミングも設計に含めます。

## 参考

- [functools.cached_property](https://docs.python.org/ja/3.14/library/functools.html#functools.cached_property)
