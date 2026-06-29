---
title: "106: 署名は一定時間で比べる"
description: "hmacでメッセージ署名を作り、compare_digestで検証する。"
difficulty: 4
---

# 106: 署名は一定時間で比べる

[ヒント](../hints/106-hmac-signature-check.md) / [解答](../solutions/106-hmac-signature-check.md)

**難易度:** ☆☆☆☆

## 問題

関数 `sign_message(secret, message)` と `verify_signature(secret, message, signature)` を書いてください。

`sign_message` は、秘密鍵とメッセージからHMAC-SHA256署名を作ります。
`verify_signature` は、署名が正しいかどうかを真偽値で返します。

## 制約

- `hmac` と `hashlib.sha256` を使ってください。
- `secret` と `message` は `bytes` です。
- `sign_message` の戻り値は16進文字列です。
- `verify_signature` では、通常の `==` ではなく `hmac.compare_digest` を使ってください。
- `signature` は16進文字列です。

## 例

```python
>>> signature = sign_message(b"key", b"data")
>>> len(signature)
64
>>> verify_signature(b"key", b"data", signature)
True
>>> verify_signature(b"key", b"other", signature)
False
```

## 発展

署名に有効期限を含める形式を設計してください。

## 参考

- [hmac](https://docs.python.org/ja/3.14/library/hmac.html)
