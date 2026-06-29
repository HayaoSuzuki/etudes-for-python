---
title: "044: バイト列の指紋を取る"
description: "hashlibでバイト列またはファイル風オブジェクトのSHA-256ダイジェストを求める。"
difficulty: 3
---

# 044: バイト列の指紋を取る

[ヒント](../hints/044-hashlib-file-digest.md) / [解答](../solutions/044-hashlib-file-digest.md)

**難易度:** ☆☆☆

## 問題

関数 `sha256_digest(source, chunk_size=8192)` を書いてください。

`source` がバイト列なら、そのSHA-256ダイジェストを返します。
`source` がファイル風オブジェクトなら、`read()` で少しずつ読みながらSHA-256ダイジェストを返します。

## 制約

- `hashlib.sha256` を使ってください。
- 戻り値は16進文字列です。
- `source` が `bytes` の場合は、そのまま処理してください。
- ファイル風オブジェクトは、`read(size)` がバイト列を返すものとします。
- ファイル風オブジェクトを読む場合は、`chunk_size` ずつ読んでください。
- `chunk_size` が0以下の場合は `ValueError` を送出してください。

## 例

```python
>>> sha256_digest(b"abc")
'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad'
>>> from io import BytesIO
>>> sha256_digest(BytesIO(b"abc"))
'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad'
```

## 発展

SHA-256以外のアルゴリズムも選べるようにしてください。

## 参考

- [hashlib](https://docs.python.org/ja/3.14/library/hashlib.html)

