---
title: "095: 「四角い三角関係」の解答"
description: "平方数を生成し、8x+1が平方数かどうかで三角数を判定する。"
difficulty: 4
---

# 095: 「四角い三角関係」の解答

[問題](../problems/095-square-triangular-number.md) / [ヒント](../hints/095-square-triangular-number.md)

**難易度:** ☆☆☆☆

## 方針

すべての正の整数を調べる必要はありません。
平方三角数は平方数なので、まず平方数だけを候補にします。

次に、候補 `x` が三角数かどうかを判定します。
`x = k * (k + 1) // 2` なら、両辺を8倍して1を足すと `8 * x + 1 = (2 * k + 1) ** 2` です。
したがって、`8 * x + 1` が平方数なら、`x` は三角数です。

## 実装

```python
from math import isqrt


def is_square(n: int) -> bool:
    root = isqrt(n)
    return root * root == n


def is_triangular(n: int) -> bool:
    return is_square(8 * n + 1)


def square_triangular_numbers(count: int) -> list[int]:
    result = []
    side = 1

    while len(result) < count:
        candidate = side * side

        if is_triangular(candidate):
            result.append(candidate)

        side += 1

    return result
```

## 確認

```python
assert square_triangular_numbers(1) == [1]
assert square_triangular_numbers(3) == [1, 36, 1225]
assert square_triangular_numbers(10) == [
    1,
    36,
    1225,
    41616,
    1413721,
    48024900,
    1631432881,
    55420693056,
    1882672131025,
    63955431761796,
]
```

## 発展

この実装は、平方数だけを候補にすることで探索範囲を大きく減らしています。
さらに大きい平方三角数を求める場合は、平方三角数そのものを生成する漸化式を使う方法もあります。

