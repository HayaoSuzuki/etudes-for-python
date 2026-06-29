---
title: "013: 七桁の住所不定"
description: "空白やハイフンを除いた7桁の数字を郵便番号形式に整える。"
difficulty: 2
---

# 013: 七桁の住所不定

[ヒント](../hints/013-postal-code.md) / [解答](../solutions/013-postal-code.md)

**難易度:** ☆☆

## 問題

関数 `format_postal_code(text)` を書いてください。
この関数は、文字列 `text` から空白とハイフンを取り除き、7桁の数字だけになった場合は `"123-4567"` の形式で返します。

7桁の数字にならない場合は `None` を返してください。

## 制約

- `text` は文字列です。
- 取り除くのは半角スペースとハイフン `-` だけです。

## 例

```python
>>> format_postal_code("1234567")
'123-4567'
>>> format_postal_code("123-4567")
'123-4567'
>>> format_postal_code(" 123 4567 ")
'123-4567'
>>> format_postal_code("12A4567") is None
True
```

## 発展

全角数字も受け付ける版を考えてください。

