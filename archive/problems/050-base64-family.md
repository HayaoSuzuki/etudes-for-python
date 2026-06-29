---
title: "050: 64文字の手紙"
description: "Base64系のエンコードとデコードを実装する。"
difficulty: 5
---

# 050: 64文字の手紙

[ヒント](../hints/050-base64-family.md) / [解答](../solutions/050-base64-family.md)

**難易度:** ☆☆☆☆☆

## 問題

Base64は、バイト列を64種類の文字で表す符号化です。

関数 `base64_encode(data, alphabet=STANDARD_ALPHABET, padding=True)` と `base64_decode(text, alphabet=STANDARD_ALPHABET)` を書いてください。

`base64_encode` は、バイト列 `data` をBase64文字列に変換します。
`base64_decode` は、Base64文字列 `text` を元のバイト列に戻します。

標準のアルファベットは、次の文字列とします。

```python
STANDARD_ALPHABET = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
```

URLの一部として扱いやすい変種として、次のアルファベットにも対応してください。

```python
URLSAFE_ALPHABET = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789-_"
```

ただし、`base64` モジュールは使わないでください。

## 仕様

- `data` は `bytes` です。
- `base64_encode` の返り値は `str` です。
- `base64_decode` の返り値は `bytes` です。
- `alphabet` は64文字の文字列です。
- 入力の長さが3の倍数でない場合、`base64_encode` は末尾に `=` を補います。
- `padding=False` の場合、`base64_encode` は末尾の `=` を取り除きます。
- `base64_decode` は、末尾の `=` が省略された文字列も受け付けます。
- 不正な文字、長さ、`=` の位置を見つけた場合は `ValueError` を送出します。

## 例

```python
>>> base64_encode(b"")
''
>>> base64_encode(b"f")
'Zg=='
>>> base64_encode(b"fo")
'Zm8='
>>> base64_encode(b"foo")
'Zm9v'
>>> base64_decode("Zm9v")
b'foo'
>>> base64_encode(b"\xfb\xff")
'+/8='
>>> base64_encode(b"\xfb\xff", URLSAFE_ALPHABET)
'-_8='
>>> base64_encode(b"\xfb\xff", URLSAFE_ALPHABET, padding=False)
'-_8'
>>> base64_decode("-_8", URLSAFE_ALPHABET)
b'\xfb\xff'
```
