---
title: "102: 「1+1=?」の解答"
description: "値を2で割った余りに正規化し、F2の演算を特殊メソッドで定義する。"
difficulty: 4
---

# 102: 「1+1=?」の解答

[問題](../problems/102-one-plus-one.md) / [ヒント](../hints/102-one-plus-one.md)

**難易度:** ☆☆☆☆

## 方針

`F2` の値は、常に `0` または `1` です。
コンストラクタで `value % 2` を保存すれば、どの整数から作っても `F2` の要素になります。

加法、減法、乗法は、計算してからもう一度 `F2` に渡します。
これで結果も必ず `0` または `1` に戻ります。

`F2` では、`1` だけが乗法逆元を持ちます。
`0` の逆元は存在しないので、`ZeroDivisionError` を送出します。

## 実装

```python
class F2:
    def __init__(self, value: int) -> None:
        self.value = value % 2

    def __repr__(self) -> str:
        return f"F2({self.value})"

    def __int__(self) -> int:
        return self.value

    def __eq__(self, other: object) -> bool:
        if not isinstance(other, F2):
            return NotImplemented
        return self.value == other.value

    def __hash__(self) -> int:
        return hash(self.value)

    def __add__(self, other: "F2") -> "F2":
        if not isinstance(other, F2):
            return NotImplemented
        return F2(self.value + other.value)

    def __neg__(self) -> "F2":
        return self

    def __sub__(self, other: "F2") -> "F2":
        if not isinstance(other, F2):
            return NotImplemented
        return self + other

    def __mul__(self, other: "F2") -> "F2":
        if not isinstance(other, F2):
            return NotImplemented
        return F2(self.value * other.value)

    def inverse(self) -> "F2":
        if self.value == 0:
            raise ZeroDivisionError("0 has no inverse in F2")
        return F2(1)

    def __truediv__(self, other: "F2") -> "F2":
        if not isinstance(other, F2):
            return NotImplemented
        return self * other.inverse()
```

## 確認

```python
zero = F2(0)
one = F2(1)

assert repr(zero) == "F2(0)"
assert repr(one) == "F2(1)"
assert int(zero) == 0
assert int(one) == 1

assert F2(2) == zero
assert F2(3) == one
assert F2(-1) == one

assert zero + zero == zero
assert zero + one == one
assert one + zero == one
assert one + one == zero

assert zero * zero == zero
assert zero * one == zero
assert one * zero == zero
assert one * one == one

assert -zero == zero
assert -one == one
assert one - one == zero
assert zero - one == one

assert one.inverse() == one
assert one / one == one

try:
    zero.inverse()
except ZeroDivisionError:
    pass
else:
    raise AssertionError("F2(0).inverse() must raise ZeroDivisionError")

try:
    one / zero
except ZeroDivisionError:
    pass
else:
    raise AssertionError("division by F2(0) must raise ZeroDivisionError")
```

## 考え方

`F2` の加法は、2を法とする整数の加法です。
そのため、`1 + 1` は `2` ではなく `0` になります。

同じ `0` と `1` を扱っていても、有限体とブール代数では演算の名前と役割が違います。
この問題では、体としての加法、減法、乗法、除法だけを実装しました。
