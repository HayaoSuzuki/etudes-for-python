---
title: "011: 「G.C.D」の解答"
description: "余りが0になるまで2つの数を更新する。"
---

# 011: 「G.C.D」の解答

[問題](../problems/011-euclidean-algorithm.md) / [ヒント](../hints/011-euclidean-algorithm.md)

## 方針

Euclidの互除法では、`gcd(a, b) = gcd(b, a % b)` を使います。
この置き換えを繰り返すと、2つ目の数が0になります。

2つ目の数が0になったとき、1つ目の数が最大公約数です。

## 実装

```python
def gcd(a: int, b: int) -> int:
    if a < 0 or b < 0:
        raise ValueError("a and b must be non-negative")
    if a == 0 and b == 0:
        raise ValueError("gcd(0, 0) is undefined")

    while b != 0:
        a, b = b, a % b

    return a
```

## 確認

```python
assert gcd(48, 18) == 6
assert gcd(1071, 462) == 21
assert gcd(0, 5) == 5
assert gcd(17, 13) == 1
assert gcd(17, 3120) == 1
assert gcd(18, 3120) == 6
```

## 考え方

`a` を `b` で割った余りを `r` とします。
`a` と `b` をどちらも割り切る数は、`b` と `r` も割り切ります。
そのため、`gcd(a, b)` を `gcd(b, r)` に置き換えても最大公約数は変わりません。

この置き換えでは2つ目の数が小さくなるので、やがて余りは0になります。
