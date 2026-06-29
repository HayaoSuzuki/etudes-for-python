---
title: "001: 「釣りはいらねえ、とは言えなくて」の解答"
description: "支払額と合計金額から、おつりを求める。"
difficulty: 1
---

# 001: 「釣りはいらねえ、とは言えなくて」の解答

[問題](../problems/001-change-due.md) / [ヒント](../hints/001-change-due.md)

**難易度:** ☆

## 方針

おつりは、支払額と合計金額の差です。
入力では `paid >= total` が保証されているので、そのまま引き算します。

## 実装

```python
def change_due(total, paid):
    return paid - total
```

## 確認

```python
assert change_due(380, 500) == 120
assert change_due(1000, 1000) == 0
assert change_due(0, 10) == 10
```

## 発展

支払額が足りない入力も扱うなら、先に条件を確認します。

```python
def change_due_checked(total, paid):
    if paid < total:
        raise ValueError("paid must be greater than or equal to total")
    return paid - total
```

