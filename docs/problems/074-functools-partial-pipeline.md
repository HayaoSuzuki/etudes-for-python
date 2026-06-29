---
title: "074: 設定済みの整形関数を作る"
description: "functools.partialで引数を固定した文字列整形関数を作る。"
difficulty: 3
---

# 074: 設定済みの整形関数を作る

[ヒント](../hints/074-functools-partial-pipeline.md) / [解答](../solutions/074-functools-partial-pipeline.md)

**難易度:** ☆☆☆

## 問題

関数 `format_message(text, prefix="", suffix="", uppercase=False)` と `make_formatter(prefix="", suffix="", uppercase=False)` を書いてください。

`format_message` は、文字列を必要に応じて大文字にし、前後に文字列を付けます。
`make_formatter` は、設定済みの整形関数を返します。

## 制約

- `make_formatter` では `functools.partial` を使ってください。
- `uppercase` が `True` の場合は、本文を大文字にしてください。
- `prefix` と `suffix` は、変換後の本文の前後に付けてください。
- `make_formatter(...)` の戻り値は、文字列1つを受け取る呼び出し可能オブジェクトです。

## 例

```python
>>> format_message("ok", prefix="[", suffix="]", uppercase=True)
'[OK]'
>>> warn = make_formatter(prefix="WARN: ", uppercase=True)
>>> warn("disk low")
'WARN: DISK LOW'
```

## 発展

複数の整形関数を順に適用するパイプラインを作ってください。

## 参考

- [functools.partial](https://docs.python.org/ja/3.14/library/functools.html#functools.partial)

