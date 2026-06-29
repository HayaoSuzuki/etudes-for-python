---
title: "077: 「出口で例外を見分ける」の解答"
description: "__exit__の返り値で特定の例外だけを抑制する。"
difficulty: 4
---

# 077: 「出口で例外を見分ける」の解答

[問題](../problems/077-suppress-only.md) / [ヒント](../hints/077-suppress-only.md)

**難易度:** ☆☆☆☆

## 方針

`__exit__` で、発生した例外型が指定された例外型のサブクラスかどうかを調べます。
対象なら例外オブジェクトを保存し、`True` を返して抑制します。
対象でなければ `False` を返します。

## 実装

```python
class SuppressOnly:
    def __init__(self, exception_type):
        self.exception_type = exception_type
        self.suppressed = None

    def __enter__(self):
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        if exc_type is not None and issubclass(exc_type, self.exception_type):
            self.suppressed = exc_value
            return True
        return False
```

## 確認

```python
with SuppressOnly(ValueError) as guard:
    raise ValueError("bad")
assert str(guard.suppressed) == "bad"

try:
    with SuppressOnly(ValueError):
        raise TypeError("wrong")
except TypeError as exc:
    assert str(exc) == "wrong"
else:
    raise AssertionError("TypeError was not raised")
```

## 発展

複数の例外型を受け取れるようにしてください。
`except` 節と同じように、例外型のタプルを `issubclass()` に渡せます。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/compound_stmts.html#the-with-statement)

