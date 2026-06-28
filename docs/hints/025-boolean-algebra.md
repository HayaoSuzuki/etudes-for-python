---
title: "025: 「ブールの箱庭」のヒント"
description: "冪集合を使って、ブール代数の演算と法則を実装する。"
---

# 025: 「ブールの箱庭」のヒント

[問題](../problems/025-boolean-algebra.md) / [解答](../solutions/025-boolean-algebra.md)

??? tip "ヒント1"

    要素を変更できる `set` のまま返すと、あとから中身が変わってしまいます。
    ブール代数の要素として扱う値は、`frozenset` にしておくと安全です。

??? tip "ヒント2"

    和は `a | b`、積は `a & b`、補元は `universe - a` で実装できます。
    ただし、演算の前に `a` と `b` が `universe` の部分集合であることを確認します。

??? tip "ヒント3"

    `elements()` では、`universe` のすべての部分集合を列挙します。
    `itertools.combinations` を使うと、サイズ0からサイズ `len(universe)` までの組み合わせを作れます。

??? tip "ヒント4"

    `check_boolean_laws` は、全要素の組み合わせを調べれば実装できます。
    交換律と冪等律は1つまたは2つの要素、分配律は3つの要素を使って確認します。
