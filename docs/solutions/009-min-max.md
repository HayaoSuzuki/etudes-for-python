---
title: "009: 「リストの両端に王がいる」の解答"
description: "数値のリストを走査し、最小値と最大値を返す。"
difficulty: 2
---

# 009: 「リストの両端に王がいる」の解答

[問題](../problems/009-min-max.md) / [ヒント](../hints/009-min-max.md)

**難易度:** ☆☆

## 方針

最初の要素を、いったん最小値でも最大値でもあるものとして扱います。
そのあと、残りの要素を1つずつ見て、必要なら値を更新します。

## 実装

```python
def min_max(numbers):
    smallest = numbers[0]
    largest = numbers[0]

    for number in numbers[1:]:
        if number < smallest:
            smallest = number
        if number > largest:
            largest = number

    return (smallest, largest)
```

## 確認

```python
assert min_max([3, 1, 4, 1, 5]) == (1, 5)
assert min_max([-2, -8, 0]) == (-8, 0)
assert min_max([7]) == (7, 7)
```

## 発展

空のリストも扱うなら、最初に長さを確認します。

```python
def min_max_checked(numbers):
    if len(numbers) == 0:
        raise ValueError("numbers must not be empty")
    return min_max(numbers)
```

