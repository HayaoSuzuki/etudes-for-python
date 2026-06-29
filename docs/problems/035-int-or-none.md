---
title: "035: 42か、それ以外か"
description: "文字列を整数へ変換し、失敗したらNoneを返す。"
difficulty: 2
---

# 035: 42か、それ以外か

[ヒント](../hints/035-int-or-none.md) / [解答](../solutions/035-int-or-none.md)

**難易度:** ☆☆

## 問題

関数 `int_or_none(text)` を書いてください。
この関数は、文字列 `text` を整数に変換できる場合はその整数を返し、変換できない場合は `None` を返します。

前後の空白は無視してください。

## 制約

- `text` は文字列です。
- 整数に変換できない入力では、例外を外へ出さずに `None` を返します。
- 小数は整数に変換できないものとして扱います。

## 例

```python
>>> int_or_none("42")
42
>>> int_or_none("  -7  ")
-7
>>> int_or_none("3.14") is None
True
>>> int_or_none("hello") is None
True
```

## 発展

`parse_scores` に応用して、変換できる項目だけを集める関数を書いてください。
