---
title: "078: 例外には親がいる"
description: "raise fromで変換前の例外を__cause__として残す。"
difficulty: 4
---

# 078: 例外には親がいる

[ヒント](../hints/078-exception-cause.md) / [解答](../solutions/078-exception-cause.md)

**難易度:** ☆☆☆☆

## 問題

関数 `parse_required_int(record, key)` を書いてください。
この関数は、辞書 `record` から `key` に対応する値を取り出し、整数に変換して返します。

`key` が存在しない場合は、`KeyError("missing field: key")` を送出してください。
値を整数に変換できない場合は、`ValueError("invalid integer field: key")` を送出してください。
どちらの場合も、原因になった元の例外を `raise ... from ...` で `__cause__` に残してください。

## 制約

- `record` は辞書です。
- `key` は文字列です。
- 整数への変換には `int()` を使います。
- 例外メッセージ中の `key` は、実際のキー文字列に置き換えてください。

## 例

```python
>>> parse_required_int({"age": "42"}, "age")
42
>>> try:
...     parse_required_int({}, "age")
... except KeyError as exc:
...     type(exc.__cause__).__name__
'KeyError'
>>> try:
...     parse_required_int({"age": "forty"}, "age")
... except ValueError as exc:
...     type(exc.__cause__).__name__
'ValueError'
```

## 参考

- [`raise` 文](https://docs.python.org/ja/3.14/reference/simple_stmts.html#the-raise-statement)

