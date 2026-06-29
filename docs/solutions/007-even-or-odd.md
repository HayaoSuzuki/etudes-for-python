---
title: "007: 「驚くべき関数」の解答"
description: "2で割り切れないことを使って奇数を判定する。"
difficulty: 1
---

# 007: 「驚くべき関数」の解答

[問題](../problems/007-even-or-odd.md) / [ヒント](../hints/007-even-or-odd.md)

**難易度:** ☆

## 方針

奇数は、2で割り切れない整数です。
したがって、2で割った余りが0ではないことを判定します。

Pythonでは `-3 % 2` は `1` なので、`n % 2 == 1` でもこの例は通ります。
ただし、剰余の符号規則が違う言語では、負の奇数の余りが `-1` になることがあります。
奇数の条件は「余りが1」ではなく、「余りが0ではない」と書くほうが定義に近くなります。

## 実装

```python
def is_odd(n: int) -> bool:
    return n % 2 != 0
```

## 確認

```python
assert is_odd(3) is True
assert is_odd(4) is False
assert is_odd(0) is False
assert is_odd(-3) is True
```

## 発展

偶数判定は、奇数判定の否定として書けます。

```python
def is_even(n: int) -> bool:
    return not is_odd(n)
```
