---
title: "025: 「偽ならそのまま帰る」の解答"
description: "andとorが真偽値ではなく評価された値を返すことを確かめる。"
difficulty: 3
---

# 025: 「偽ならそのまま帰る」の解答

[問題](../problems/025-boolean-operands-return.md) / [ヒント](../hints/025-boolean-operands-return.md)

**難易度:** ☆☆☆

## 方針

`and` と `or` の結果を、変換せずにそのまま返します。
`not` だけは、Pythonの仕様として `True` または `False` を返します。

## 実装

```python
def boolean_operands(a, b):
    return {
        "or": a or b,
        "and": a and b,
        "not": not a,
    }
```

## 確認

```python
assert boolean_operands("", "fallback") == {"or": "fallback", "and": "", "not": True}
assert boolean_operands("name", "fallback") == {"or": "name", "and": "fallback", "not": False}
assert boolean_operands([], [1, 2]) == {"or": [1, 2], "and": [], "not": True}
```

## 発展

`a and b or c` は、`b` が偽と解釈される値のときに条件式の代わりになりません。
その挙動を例で確認してください。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#boolean-operations)
