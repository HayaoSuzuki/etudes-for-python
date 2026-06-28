---
title: "007: アッカーマン関数の解答"
description: "m=3に固定して閉じた式へ変形し、大きなnまで計算する。"
---

# 007: アッカーマン関数の解答

[問題](../problems/007-ackermann-function.md) / [ヒント](../hints/007-ackermann-function.md)

## 方針

定義をそのまま一般の再帰関数に写すと、`m = 3` でも大きな `n` では扱いにくくなります。
`m = 3` に固定し、下の段から順に式を整理します。

`A(0, n)` は `n + 1` です。
そこから順に計算すると、次の式が得られます。

- `A(1, n) = n + 2`
- `A(2, n) = 2 * n + 3`
- `A(3, n) = 2 ** (n + 3) - 3`

したがって、`A(3, n)` は再帰呼び出しを使わずに計算できます。

## 実装

```python
def ackermann_3(n: int) -> int:
    return 2 ** (n + 3) - 3
```

## 確認

```python
assert ackermann_3(0) == 5
assert ackermann_3(1) == 13
assert ackermann_3(2) == 29
assert ackermann_3(3) == 61
assert ackermann_3(10) == 8189
assert ackermann_3(100) == 10141204801825835211973625643005
assert ackermann_3(10000).bit_length() == 10003
assert len(str(ackermann_3(10000))) == 3012
```

## 別解

閉じた式を使わず、`A(3, n) = 2 * A(3, n - 1) + 3` を前から計算してもよいです。
この方法でも、一般の再帰定義を直接呼び出すよりずっと安定します。

```python
def ackermann_3_iterative(n: int) -> int:
    value = 5

    for _ in range(n):
        value = 2 * value + 3

    return value
```

```python
assert ackermann_3_iterative(10) == 8189
assert ackermann_3_iterative(10000) == ackermann_3(10000)
```
