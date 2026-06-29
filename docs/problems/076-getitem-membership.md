---
title: "076: inは古い扉も叩く"
description: "__contains__も__iter__もないオブジェクトでmembership testを成立させる。"
difficulty: 4
---

# 076: inは古い扉も叩く

[ヒント](../hints/076-getitem-membership.md) / [解答](../solutions/076-getitem-membership.md)

**難易度:** ☆☆☆☆

## 問題

クラス `SquaresBelow` を書いてください。
このクラスは、`0 ** 2` から `(limit - 1) ** 2` までの平方数を持つシーケンスのように振る舞います。

ただし、実装する特殊メソッドは `__getitem__` だけにしてください。
`__contains__` と `__iter__` は実装しません。

## 制約

- `limit` は0以上の整数です。
- `obj[index]` は `index ** 2` を返します。
- `index` が0以上 `limit` 未満でない場合は `IndexError` を送出します。
- `x in obj` が使えるようにしてください。

## 例

```python
>>> squares = SquaresBelow(5)
>>> squares[3]
9
>>> 16 in squares
True
>>> 25 in squares
False
>>> list(squares)
[0, 1, 4, 9, 16]
```

## 参考

- [帰属検査演算](https://docs.python.org/ja/3.14/reference/expressions.html#membership-test-operations)

