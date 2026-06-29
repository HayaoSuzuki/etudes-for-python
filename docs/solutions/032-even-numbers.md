---
title: "032: 「二で割り切れる者たち」の解答"
description: "整数のリストから偶数だけを取り出す。"
difficulty: 2
---

# 032: 「二で割り切れる者たち」の解答

[問題](../problems/032-even-numbers.md) / [ヒント](../hints/032-even-numbers.md)

**難易度:** ☆☆

## 方針

入力のリストを1つずつ調べます。
偶数なら結果用のリストに追加し、最後にそのリストを返します。

## 実装

```python
def even_numbers(numbers):
    result = []
    for number in numbers:
        if number % 2 == 0:
            result.append(number)
    return result
```

## 確認

```python
assert even_numbers([1, 2, 3, 4, 5, 6]) == [2, 4, 6]
assert even_numbers([1, 3, 5]) == []
assert even_numbers([-2, -1, 0, 1, 2]) == [-2, 0, 2]
```

## 発展

奇数だけを返す場合は、条件を `number % 2 != 0` に変えます。
