---
title: "020: 名前順では勝てない表彰台"
description: "名前と点数の組を、点数順と名前順で並べる。"
difficulty: 3
---

# 020: 名前順では勝てない表彰台

[ヒント](../hints/020-score-podium.md) / [解答](../solutions/020-score-podium.md)

**難易度:** ☆☆☆

## 問題

関数 `podium(records, limit=3)` を書いてください。
この関数は、`(name, score)` のタプルのリストを受け取り、上位 `limit` 人の名前をリストで返します。

点数が高い人ほど上位です。
点数が同じ場合は、名前の辞書順で早い人を先にしてください。

## 制約

- `name` は文字列です。
- `score` は整数です。
- `limit` は0以上の整数です。
- 元の `records` は変更しません。

## 例

```python
>>> podium([("Ada", 90), ("Bob", 95), ("Cyd", 95), ("Dee", 80)])
['Bob', 'Cyd', 'Ada']
>>> podium([("Mika", 10), ("Aki", 10)], 1)
['Aki']
>>> podium([], 3)
[]
```

## 発展

返り値を名前だけではなく、`(name, score)` のタプルのままにする版も書いてください。
