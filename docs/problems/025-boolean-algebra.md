---
title: "025: ブールの箱庭"
description: "有限集合の冪集合としてブール代数を実装する。"
---

# 025: ブールの箱庭

[ヒント](../hints/025-boolean-algebra.md) / [解答](../solutions/025-boolean-algebra.md)

## 問題

**ブール代数**を、有限集合の冪集合として実装してください。

集合 `universe` を全体集合とします。
この問題では、`universe` の部分集合をブール代数の要素として扱います。
和、積、補元は、それぞれ和集合、共通部分、補集合として実装します。

クラス `PowerSetBooleanAlgebra` を書いてください。
このクラスは、次のメソッドを持ちます。

- `element(values)`：`values` を `frozenset` にして返す
- `elements()`：全要素、つまり `universe` のすべての部分集合を返す
- `bottom()`：最小元、つまり空集合を返す
- `top()`：最大元、つまり全体集合を返す
- `join(a, b)`：和を返す
- `meet(a, b)`：積を返す
- `complement(a)`：補元を返す
- `leq(a, b)`：`a` が `b` 以下かどうかを返す

`values` や演算の引数に `universe` に含まれない値がある場合は、`ValueError` を送出してください。

さらに、関数 `check_boolean_laws(algebra)` を書いてください。
この関数は、次の性質がすべて成り立つとき `True` を返します。

- 交換律
- 分配律
- 冪等律
- 補元律
- 最小元と最大元の単位元としての性質

## 例

```python
>>> algebra = PowerSetBooleanAlgebra({"a", "b", "c"})
>>> a = algebra.element({"a"})
>>> b = algebra.element({"b"})
>>> ab = algebra.element({"a", "b"})
>>> bc = algebra.element({"b", "c"})
>>> algebra.join(a, b) == ab
True
>>> algebra.meet(ab, bc) == algebra.element({"b"})
True
>>> algebra.complement(a) == algebra.element({"b", "c"})
True
>>> algebra.join(a, algebra.complement(a)) == algebra.top()
True
>>> algebra.meet(a, algebra.complement(a)) == algebra.bottom()
True
>>> algebra.leq(a, ab)
True
>>> check_boolean_laws(algebra)
True
```

## 補足

前問の `F2` は、有限体として `+`、`-`、`*`、`/` を実装しました。
この問題では、ブール代数として `join`、`meet`、`complement` を実装します。
