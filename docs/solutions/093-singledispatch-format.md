---
title: "093: 「型ごとに表示を切り替える」の解答"
description: "singledispatchで型ごとの整形関数を登録する。"
difficulty: 4
---

# 093: 「型ごとに表示を切り替える」の解答

[問題](../problems/093-singledispatch-format.md) / [ヒント](../hints/093-singledispatch-format.md)

**難易度:** ☆☆☆☆

## 方針

`@singledispatch` を付けた関数を既定の実装にします。
型ごとの整形は、`@format_value.register` で追加します。

`bool` は `int` のサブクラスですが、`bool` 用の実装を登録しておけば、真偽値にはそちらが使われます。

## 実装

```python
from functools import singledispatch


@singledispatch
def format_value(value):
    return repr(value)


@format_value.register
def _(value: str):
    return f'"{value}"'


@format_value.register
def _(value: bool):
    return "true" if value else "false"


@format_value.register
def _(value: int):
    return str(value)


@format_value.register
def _(value: list):
    inner = ", ".join(format_value(item) for item in value)
    return f"[{inner}]"
```

## 確認

```python
assert format_value("hello") == '"hello"'
assert format_value(True) == "true"
assert format_value([1, "x", False]) == '[1, "x", false]'
assert format_value({"a": 1}) == "{'a': 1}"
```

## 発展

`singledispatch` は第一引数の型だけを見ます。
複数の引数の組み合わせで分岐したい場合は、別の設計が必要になります。

## 参考

- [functools.singledispatch](https://docs.python.org/ja/3.14/library/functools.html#functools.singledispatch)
