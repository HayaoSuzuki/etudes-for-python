---
title: "005: 「JSONは誰の息子」のヒント"
description: "JSONを辞書として読み、既定値と型検査を段階的に適用する。"
difficulty: 2
---

# 005: 「JSONは誰の息子」のヒント

[問題](../problems/005-json-settings-loader.md) / [解答](../solutions/005-json-settings-loader.md)

**難易度:** ☆☆
??? tip "ヒント1"

    最初に `json.loads` の結果が辞書かどうかを確認します。
    リストや文字列を受け入れると、その後のキー検査が意味を持ちません。

??? tip "ヒント2"

    未知キーは、`set(data) - allowed_keys` で見つけられます。
    エラーに出すキーを安定させたい場合は、`sorted` して先頭を使います。

??? tip "ヒント3"

    `bool` は `int` の一種として扱われます。
    `min_total` では `isinstance(value, int)` ではなく、`type(value) is int` で検査します。

??? tip "ヒント4"

    `aliases` は入れ子の辞書です。
    外側だけでなく、キーと値を1つずつ見て、どちらも文字列かどうかを確認します。