---
title: "088: 「二本の下線は名前を隠す」の解答"
description: "private name manglingの規則を関数として実装する。"
difficulty: 5
---

# 088: 「二本の下線は名前を隠す」の解答

[問題](../problems/088-private-name-mangle.md) / [ヒント](../hints/088-private-name-mangle.md)

**難易度:** ☆☆☆☆☆

## 方針

変換対象でない識別子を先に除外します。
対象になる場合は、クラス名の先頭の `_` を取り除きます。
残ったクラス名が空なら変換せず、そうでなければ `_{class_name}{identifier}` の形にします。

## 実装

```python
def mangle_private_name(class_name, identifier):
    if not identifier.startswith("__"):
        return identifier
    if identifier.endswith("__"):
        return identifier

    stripped_class_name = class_name.lstrip("_")
    if stripped_class_name == "":
        return identifier
    return "_" + stripped_class_name + identifier
```

## 確認

```python
assert mangle_private_name("Foo", "__spam") == "_Foo__spam"
assert mangle_private_name("_Foo", "__spam") == "_Foo__spam"
assert mangle_private_name("__Foo", "__spam_") == "_Foo__spam_"
assert mangle_private_name("Foo", "__spam__") == "__spam__"
assert mangle_private_name("__", "__spam") == "__spam"
assert mangle_private_name("Foo", "_spam") == "_spam"
```

## 発展

実際にクラスを定義し、`vars(クラス名)` や `vars(インスタンス)` で属性名を確認してください。
関数の結果と一致する名前が現れます。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#private-name-mangling)

