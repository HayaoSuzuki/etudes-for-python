---
title: "013: 「七桁の住所不定」の解答"
description: "空白やハイフンを除いた7桁の数字を郵便番号形式に整える。"
difficulty: 2
---

# 013: 「七桁の住所不定」の解答

[問題](../problems/013-postal-code.md) / [ヒント](../hints/013-postal-code.md)

**難易度:** ☆☆

## 方針

入力文字列を1文字ずつ見て、半角スペースとハイフン以外を残します。
残った文字列が7桁の数字なら、スライスで3桁と4桁に分けて返します。

## 実装

```python
def format_postal_code(text):
    cleaned = ""
    for ch in text:
        if ch != " " and ch != "-":
            cleaned += ch

    if len(cleaned) != 7:
        return None
    if not cleaned.isdigit():
        return None
    return cleaned[:3] + "-" + cleaned[3:]
```

## 確認

```python
assert format_postal_code("1234567") == "123-4567"
assert format_postal_code("123-4567") == "123-4567"
assert format_postal_code(" 123 4567 ") == "123-4567"
assert format_postal_code("12A4567") is None
```

## 発展

全角数字を扱う場合は、どの文字を数字として認めるかを先に決めます。
この問題では、入力の正規化までは扱いません。
