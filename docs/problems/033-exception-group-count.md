---
title: "033: 例外の束をほどく"
description: "except*でExceptionGroupを型ごとの部分グループに分ける。"
difficulty: 5
---

# 033: 例外の束をほどく

[ヒント](../hints/033-exception-group-count.md) / [解答](../solutions/033-exception-group-count.md)

**難易度:** ☆☆☆☆☆

## 問題

関数 `count_exception_group(exceptions)` を書いてください。
この関数は、例外オブジェクトのリスト `exceptions` を受け取り、例外型ごとの個数を辞書で返します。

関数内では、空でない `exceptions` から `ExceptionGroup` を作って送出し、`except*` で次の3分類に分けてください。

- `ValueError`
- `TypeError`
- その他の `Exception`

返す辞書のキーは、`"ValueError"`、`"TypeError"`、`"Other"` とします。

## 制約

- `exceptions` は `Exception` のインスタンスのリストです。
- `exceptions` が空の場合は、すべて0の辞書を返してください。
- `except*` 節の中で `return` してはいけません。

## 例

```python
>>> count_exception_group([ValueError("a"), TypeError("b"), OSError("c")])
{'ValueError': 1, 'TypeError': 1, 'Other': 1}
>>> count_exception_group([ValueError("a"), ValueError("b")])
{'ValueError': 2, 'TypeError': 0, 'Other': 0}
>>> count_exception_group([])
{'ValueError': 0, 'TypeError': 0, 'Other': 0}
```

## 参考

- [`except*` 節](https://docs.python.org/ja/3.14/reference/compound_stmts.html#except-star)
