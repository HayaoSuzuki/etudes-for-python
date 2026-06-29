---
title: "073: 番人は属性の入口に立つ"
description: "デスクリプタで属性代入を検査し、インスタンスごとに値を保存する。"
difficulty: 5
---

# 073: 番人は属性の入口に立つ

[ヒント](../hints/073-descriptor-guard.md) / [解答](../solutions/073-descriptor-guard.md)

**難易度:** ☆☆☆☆☆

## 問題

デスクリプタ `NonNegativeInteger` と、それを使うクラス `CartLine` を書いてください。

`NonNegativeInteger` は、属性に代入される値を検査します。
受け入れる値は、`bool` ではない `int` で、0以上の値だけです。

`CartLine` は、商品名、数量、単価を持つクラスです。
`quantity` と `unit_price` には `NonNegativeInteger` を使ってください。

## 制約

- `NonNegativeInteger` は `__set_name__`、`__get__`、`__set__` を実装してください。
- 値が `int` でなければ `TypeError` を送出してください。
- 値が負なら `ValueError` を送出してください。
- インスタンスごとに値を別々に保存してください。
- `CartLine.total` は、数量と単価を掛けた値を返すプロパティにしてください。

## 例

```python
>>> pen = CartLine("pen", 2, 120)
>>> notebook = CartLine("notebook", 1, 300)
>>> pen.quantity = 5
>>> pen.total
600
>>> notebook.total
300
>>> pen.quantity = -1
Traceback (most recent call last):
...
ValueError: value must be non-negative
```

## 参考

- [デスクリプタ ガイド](https://docs.python.org/ja/3.14/howto/descriptor.html)
