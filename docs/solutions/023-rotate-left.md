---
title: "023: 「スライスが回す輪」の解答"
description: "リストを左に回転し、新しいリストとして返す。"
difficulty: 2
---

# 023: 「スライスが回す輪」の解答

[問題](../problems/023-rotate-left.md) / [ヒント](../hints/023-rotate-left.md)

**難易度:** ☆☆

## 方針

空リストは先に返します。
空でない場合は、`n` をリストの長さで割った余りに直します。
その位置でリストを前半と後半に分け、順番を入れ替えて結合します。

## 実装

```python
def rotate_left(items, n):
    if items == []:
        return []

    n = n % len(items)
    return items[n:] + items[:n]
```

## 確認

```python
original = [1, 2, 3, 4]
assert rotate_left(original, 1) == [2, 3, 4, 1]
assert rotate_left(original, 5) == [2, 3, 4, 1]
assert rotate_left(original, -1) == [4, 1, 2, 3]
assert rotate_left([], 3) == []
assert original == [1, 2, 3, 4]
```

## 発展

文字列もスライスと `+` が使えるので、同じ方針で回転できます。
ただし、返り値はリストではなく文字列になります。
