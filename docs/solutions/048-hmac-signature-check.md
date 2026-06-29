---
title: "048: 「署名は一定時間で比べる」の解答"
description: "HMAC-SHA256署名を作り、compare_digestで検証する。"
difficulty: 4
---

# 048: 「署名は一定時間で比べる」の解答

[問題](../problems/048-hmac-signature-check.md) / [ヒント](../hints/048-hmac-signature-check.md)

**難易度:** ☆☆☆☆

## 方針

署名の作成では、秘密鍵、メッセージ、ハッシュ関数を指定してHMACを作ります。
検証では、同じ方法で期待される署名を作り、受け取った署名と比較します。

比較には `compare_digest` を使います。

## 実装

```python
import hashlib
import hmac


def sign_message(secret, message):
    return hmac.new(secret, message, hashlib.sha256).hexdigest()


def verify_signature(secret, message, signature):
    expected = sign_message(secret, message)
    return hmac.compare_digest(expected, signature)
```

## 確認

```python
signature = sign_message(b"key", b"data")

assert len(signature) == 64
assert verify_signature(b"key", b"data", signature) is True
assert verify_signature(b"key", b"other", signature) is False
```

## 発展

HMACは、署名を作った相手が同じ秘密鍵を持っていることを確認するために使えます。
秘密鍵をどう管理するか、署名対象に何を含めるかも重要な仕様です。

## 参考

- [hmac](https://docs.python.org/ja/3.14/library/hmac.html)

