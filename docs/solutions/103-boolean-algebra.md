---
title: "103: 「ブールの箱庭」の解答"
description: "冪集合の和集合、共通部分、補集合としてブール代数を実装する。"
difficulty: 5
---

# 103: 「ブールの箱庭」の解答

[問題](../problems/103-boolean-algebra.md) / [ヒント](../hints/103-boolean-algebra.md)

**難易度:** ☆☆☆☆☆

## 方針

有限集合 `universe` の部分集合を、ブール代数の要素として扱います。
要素は `frozenset` で表します。

和は和集合、積は共通部分、補元は `universe` に対する差集合です。
どの演算でも、引数が `universe` の部分集合であることを確認してから計算します。

ブール代数の法則は、全要素を列挙して確認できます。
有限集合の冪集合なので、すべての部分集合を作れば十分です。

## 実装

```python
from collections.abc import Iterable
from itertools import combinations


class PowerSetBooleanAlgebra:
    def __init__(self, universe: Iterable[str]) -> None:
        self.universe = frozenset(universe)

    def element(self, values: Iterable[str]) -> frozenset[str]:
        element = frozenset(values)
        if not element <= self.universe:
            raise ValueError("element must be a subset of universe")
        return element

    def elements(self) -> list[frozenset[str]]:
        items = list(self.universe)
        result = []

        for size in range(len(items) + 1):
            for selected in combinations(items, size):
                result.append(frozenset(selected))

        return result

    def bottom(self) -> frozenset[str]:
        return frozenset()

    def top(self) -> frozenset[str]:
        return self.universe

    def join(self, a: Iterable[str], b: Iterable[str]) -> frozenset[str]:
        left = self.element(a)
        right = self.element(b)
        return left | right

    def meet(self, a: Iterable[str], b: Iterable[str]) -> frozenset[str]:
        left = self.element(a)
        right = self.element(b)
        return left & right

    def complement(self, a: Iterable[str]) -> frozenset[str]:
        element = self.element(a)
        return self.universe - element

    def leq(self, a: Iterable[str], b: Iterable[str]) -> bool:
        left = self.element(a)
        right = self.element(b)
        return left <= right


def check_boolean_laws(algebra: PowerSetBooleanAlgebra) -> bool:
    elements = algebra.elements()
    bottom = algebra.bottom()
    top = algebra.top()

    for a in elements:
        if algebra.join(a, bottom) != a:
            return False
        if algebra.meet(a, top) != a:
            return False
        if algebra.join(a, a) != a:
            return False
        if algebra.meet(a, a) != a:
            return False
        if algebra.join(a, algebra.complement(a)) != top:
            return False
        if algebra.meet(a, algebra.complement(a)) != bottom:
            return False

        for b in elements:
            if algebra.join(a, b) != algebra.join(b, a):
                return False
            if algebra.meet(a, b) != algebra.meet(b, a):
                return False

            for c in elements:
                if algebra.meet(a, algebra.join(b, c)) != algebra.join(
                    algebra.meet(a, b),
                    algebra.meet(a, c),
                ):
                    return False
                if algebra.join(a, algebra.meet(b, c)) != algebra.meet(
                    algebra.join(a, b),
                    algebra.join(a, c),
                ):
                    return False

    return True
```

## 確認

```python
algebra = PowerSetBooleanAlgebra({"a", "b", "c"})
a = algebra.element({"a"})
b = algebra.element({"b"})
ab = algebra.element({"a", "b"})
bc = algebra.element({"b", "c"})

assert algebra.join(a, b) == ab
assert algebra.meet(ab, bc) == algebra.element({"b"})
assert algebra.complement(a) == algebra.element({"b", "c"})
assert algebra.join(a, algebra.complement(a)) == algebra.top()
assert algebra.meet(a, algebra.complement(a)) == algebra.bottom()
assert algebra.leq(a, ab)
assert not algebra.leq(bc, ab)

expected_elements = {
    frozenset(),
    frozenset({"a"}),
    frozenset({"b"}),
    frozenset({"c"}),
    frozenset({"a", "b"}),
    frozenset({"a", "c"}),
    frozenset({"b", "c"}),
    frozenset({"a", "b", "c"}),
}
assert set(algebra.elements()) == expected_elements
assert check_boolean_laws(algebra)

try:
    algebra.element({"x"})
except ValueError:
    pass
else:
    raise AssertionError("unknown element must raise ValueError")
```

## 考え方

冪集合で作るブール代数では、部分集合そのものが要素です。
空集合が最小元、全体集合が最大元になります。

`join` は「どちらかに含まれる」、`meet` は「両方に含まれる」、`complement` は「全体集合に含まれるが、その要素には含まれない」を表します。
この3つを集合演算として実装すると、ブール代数の法則をそのまま確認できます。

