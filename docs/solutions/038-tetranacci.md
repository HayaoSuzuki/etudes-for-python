---
title: "038: 「フィボナッチの四重奏」の解答"
description: "前から順に計算して、各項を一度だけ求める。"
difficulty: 3
---

# 038: 「フィボナッチの四重奏」の解答

[問題](../problems/038-tetranacci.md) / [ヒント](../hints/038-tetranacci.md)

**難易度:** ☆☆☆

## 方針

素朴な再帰関数では、同じ `T(k)` を何度も計算します。
`T(100)` を求めるには、各項を一度だけ計算する形に変えます。

初期値 `0, 0, 0, 1` をリストに入れ、4番目以降を前から順に追加します。
`values[k]` を作る時点では、必要な4項はすでに計算済みです。

## 実装

```python
def tetranacci(n: int) -> int:
    values = [0, 0, 0, 1]

    for k in range(4, n + 1):
        values.append(values[k - 1] + values[k - 2] + values[k - 3] + values[k - 4])

    return values[n]
```

## 確認

```python
assert tetranacci(0) == 0
assert tetranacci(1) == 0
assert tetranacci(2) == 0
assert tetranacci(3) == 1
assert tetranacci(8) == 15
assert tetranacci(10) == 56
assert tetranacci(50) == 14075762303480
assert tetranacci(100) == 2505471397838180985096739296
```

## 発展

`T(n)` だけが必要なら、すべての項をリストに残す必要はありません。
直前4項だけを持つと、使用するメモリを一定にできます。

```python
def tetranacci_compact(n: int) -> int:
    a, b, c, d = 0, 0, 0, 1

    if n == 0:
        return a
    if n == 1:
        return b
    if n == 2:
        return c
    if n == 3:
        return d

    for _ in range(4, n + 1):
        a, b, c, d = b, c, d, a + b + c + d

    return d
```

この実装でも、各項は前から一度ずつしか計算されません。

## 別解

再帰式の形を残したい場合は、`functools.lru_cache` で計算済みの値を保存できます。
同じ `T(k)` が再び必要になったとき、関数本体をもう一度実行せず、保存済みの値を返します。

```python
from functools import lru_cache


@lru_cache(maxsize=None)
def tetranacci_cached(n: int) -> int:
    if n == 0:
        return 0
    if n == 1:
        return 0
    if n == 2:
        return 0
    if n == 3:
        return 1

    return (
        tetranacci_cached(n - 1)
        + tetranacci_cached(n - 2)
        + tetranacci_cached(n - 3)
        + tetranacci_cached(n - 4)
    )
```

```python
assert tetranacci_cached(50) == 14075762303480
assert tetranacci_cached(100) == 2505471397838180985096739296
```

この方法は、再帰式をそのまま読める形で残せます。
一方で、`n` が大きくなると再帰呼び出しの深さには注意が必要です。
