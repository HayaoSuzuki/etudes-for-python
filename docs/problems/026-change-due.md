---
title: "026: 釣りはいらねえ、とは言えなくて"
description: "支払額と合計金額から、おつりを求める。"
difficulty: 1
---

# 026: 釣りはいらねえ、とは言えなくて

[ヒント](../hints/026-change-due.md) / [解答](../solutions/026-change-due.md)

**難易度:** ☆

## 問題

関数 `change_due(total, paid)` を書いてください。
この関数は、商品の合計金額 `total` と支払額 `paid` を受け取り、おつりを整数で返します。

## 制約

- `total` と `paid` は整数です。
- `0 <= total <= paid` とします。
- 通貨単位は考えず、整数の差だけを扱います。

## 例

```python
>>> change_due(380, 500)
120
>>> change_due(1000, 1000)
0
>>> change_due(0, 10)
10
```

## 発展

`paid` が `total` より小さい場合に `ValueError` を送出する版も書いてください。
