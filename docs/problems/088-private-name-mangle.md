---
title: "088: 二本の下線は名前を隠す"
description: "private name manglingの規則を関数として実装する。"
difficulty: 5
---

# 088: 二本の下線は名前を隠す

[ヒント](../hints/088-private-name-mangle.md) / [解答](../solutions/088-private-name-mangle.md)

**難易度:** ☆☆☆☆☆

## 問題

関数 `mangle_private_name(class_name, identifier)` を書いてください。
この関数は、クラス定義の中で使われる private name mangling の変換規則を、文字列に対して再現します。

変換対象は、次の条件を満たす識別子です。

- 2個以上の `_` で始まる
- 2個以上の `_` で終わらない

変換対象でない場合は、`identifier` をそのまま返してください。
変換対象の場合は、`class_name` の先頭の `_` を取り除き、`_ClassName` を `identifier` の前に付けてください。
先頭の `_` を取り除いた `class_name` が空になる場合は、変換せずに `identifier` を返してください。

## 制約

- `class_name` と `identifier` は文字列です。
- 255文字を超える場合の実装依存の切り詰めは扱いません。
- Pythonの識別子として正しいかどうかは検査しません。

## 例

```python
>>> mangle_private_name("Foo", "__spam")
'_Foo__spam'
>>> mangle_private_name("_Foo", "__spam")
'_Foo__spam'
>>> mangle_private_name("__Foo", "__spam_")
'_Foo__spam_'
>>> mangle_private_name("Foo", "__spam__")
'__spam__'
>>> mangle_private_name("__", "__spam")
'__spam'
```

## 参考

- [Private name mangling](https://docs.python.org/ja/3.14/reference/expressions.html#private-name-mangling)

