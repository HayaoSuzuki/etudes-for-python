---
title: "101: 「設定済みの整形関数を作る」の解答"
description: "partialでprefix、suffix、uppercaseを固定した関数を作る。"
difficulty: 3
---

# 101: 「設定済みの整形関数を作る」の解答

[問題](../problems/101-functools-partial-pipeline.md) / [ヒント](../hints/101-functools-partial-pipeline.md)

**難易度:** ☆☆☆

## 方針

`format_message` は、本文の変換と前後の文字列付加を担当します。
`make_formatter` では、その引数の一部を `partial` で固定します。

## 実装

```python
from functools import partial


def format_message(text, prefix="", suffix="", uppercase=False):
    if uppercase:
        text = text.upper()
    return f"{prefix}{text}{suffix}"


def make_formatter(prefix="", suffix="", uppercase=False):
    return partial(
        format_message,
        prefix=prefix,
        suffix=suffix,
        uppercase=uppercase,
    )
```

## 確認

```python
assert format_message("ok", prefix="[", suffix="]", uppercase=True) == "[OK]"

warn = make_formatter(prefix="WARN: ", uppercase=True)
assert warn("disk low") == "WARN: DISK LOW"
```

## 発展

`partial` は、コールバックに追加情報を持たせたい場合にも使えます。
ただし、固定する引数が増えすぎると、普通の関数やクラスに名前を付けたほうが読みやすくなります。

## 参考

- [functools.partial](https://docs.python.org/ja/3.14/library/functools.html#functools.partial)
