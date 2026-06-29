---
title: "084: 型ごとに表示を切り替える"
description: "functools.singledispatchで値の型に応じた表示文字列を作る。"
difficulty: 4
---

# 084: 型ごとに表示を切り替える

[ヒント](../hints/084-singledispatch-format.md) / [解答](../solutions/084-singledispatch-format.md)

**難易度:** ☆☆☆☆

## 問題

関数 `format_value(value)` を書いてください。

この関数は、値の型に応じて表示用の文字列を返します。

## 制約

- `functools.singledispatch` を使ってください。
- 未登録の型では `repr(value)` を返してください。
- `str` は、二重引用符で囲んだ文字列にしてください。
- `bool` は、`true` または `false` を返してください。
- `int` は、10進整数の文字列を返してください。
- `list` は、各要素を `format_value` で整形し、`[a, b]` の形にしてください。
- `bool` は `int` のサブクラスですが、真偽値として扱ってください。

## 例

```python
>>> format_value("hello")
'"hello"'
>>> format_value(True)
'true'
>>> format_value([1, "x", False])
'[1, "x", false]'
>>> format_value({"a": 1})
"{'a': 1}"
```

## 発展

辞書も `{key: value}` の形で再帰的に整形してください。

## 参考

- [functools.singledispatch](https://docs.python.org/ja/3.14/library/functools.html#functools.singledispatch)

