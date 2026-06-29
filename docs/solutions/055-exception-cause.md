---
title: "055: 「例外には親がいる」の解答"
description: "raise fromで変換前の例外を__cause__として残す。"
difficulty: 4
---

# 055: 「例外には親がいる」の解答

[問題](../problems/055-exception-cause.md) / [ヒント](../hints/055-exception-cause.md)

**難易度:** ☆☆☆☆

## 方針

まず、辞書から値を取り出します。
キーがなければ、元の `KeyError` を原因として新しい `KeyError` を送出します。
次に `int()` で変換し、失敗した場合は元の例外を原因として `ValueError` を送出します。

## 実装

```python
def parse_required_int(record, key):
    try:
        value = record[key]
    except KeyError as exc:
        raise KeyError(f"missing field: {key}") from exc

    try:
        return int(value)
    except (TypeError, ValueError) as exc:
        raise ValueError(f"invalid integer field: {key}") from exc
```

## 確認

```python
assert parse_required_int({"age": "42"}, "age") == 42

try:
    parse_required_int({}, "age")
except KeyError as exc:
    assert str(exc) == "'missing field: age'"
    assert isinstance(exc.__cause__, KeyError)
else:
    raise AssertionError("KeyError was not raised")

try:
    parse_required_int({"age": "forty"}, "age")
except ValueError as exc:
    assert str(exc) == "invalid integer field: age"
    assert isinstance(exc.__cause__, ValueError)
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

`from None` を使うと、例外の文脈表示を抑制できます。
この問題では原因を残すことが目的なので、`from None` は使いません。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/simple_stmts.html#the-raise-statement)
