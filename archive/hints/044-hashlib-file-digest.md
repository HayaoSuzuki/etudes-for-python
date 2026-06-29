---
title: "044: 「バイト列の指紋を取る」のヒント"
description: "hashlibでバイト列またはファイル風オブジェクトのSHA-256ダイジェストを求める。"
difficulty: 3
---

# 044: 「バイト列の指紋を取る」のヒント

[問題](../problems/044-hashlib-file-digest.md) / [解答](../solutions/044-hashlib-file-digest.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `hashlib.sha256()` はハッシュオブジェクトを作ります。
    `update(bytes)` でデータを追加できます。

??? tip "ヒント2"

    バイト列が直接渡された場合は、1回だけ `update` すれば十分です。

??? tip "ヒント3"

    ファイル風オブジェクトでは、`read(chunk_size)` を繰り返します。
    空のバイト列が返ったら終わりです。

??? tip "ヒント4"

    最後に `hexdigest()` を呼ぶと、16進文字列のダイジェストが得られます。

