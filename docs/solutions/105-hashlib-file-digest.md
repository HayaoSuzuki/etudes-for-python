---
title: "105: 「バイト列の指紋を取る」の解答"
description: "sha256を作り、バイト列またはチャンク読み込みでupdateする。"
difficulty: 3
---

# 105: 「バイト列の指紋を取る」の解答

[問題](../problems/105-hashlib-file-digest.md) / [ヒント](../hints/105-hashlib-file-digest.md)

**難易度:** ☆☆☆

## 方針

`hashlib.sha256()` でハッシュオブジェクトを作ります。
入力がバイト列ならそのまま `update` します。
ファイル風オブジェクトなら、指定サイズで読みながら `update` します。

## 実装

```python
import hashlib


def sha256_digest(source, chunk_size=8192):
    if chunk_size <= 0:
        raise ValueError("chunk_size must be positive")

    digest = hashlib.sha256()
    if isinstance(source, bytes):
        digest.update(source)
    else:
        while True:
            chunk = source.read(chunk_size)
            if not chunk:
                break
            digest.update(chunk)

    return digest.hexdigest()
```

## 確認

```python
from io import BytesIO


EXPECTED = "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad"

assert sha256_digest(b"abc") == EXPECTED
assert sha256_digest(BytesIO(b"abc")) == EXPECTED

try:
    sha256_digest(b"abc", chunk_size=0)
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

ハッシュ値は、データが同じかどうかを確認する用途に使えます。
ただし、秘密情報の検証には単なるハッシュではなくHMACのような仕組みが必要です。

## 参考

- [hashlib](https://docs.python.org/ja/3.14/library/hashlib.html)
