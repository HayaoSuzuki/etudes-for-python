---
title: "049: 「メールから件名を取り出す」のヒント"
description: "emailパッケージでメール文字列を解析し、主要ヘッダーと本文を取り出す。"
difficulty: 4
---

# 049: 「メールから件名を取り出す」のヒント

[問題](../problems/049-email-header-parser.md) / [解答](../solutions/049-email-header-parser.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `email.parser.Parser` に `policy=policy.default` を渡すと、扱いやすい `EmailMessage` として解析できます。

??? tip "ヒント2"

    ヘッダーは `message["Subject"]` のように読めます。
    ない場合は `None` になるので、空文字列へ変換します。

??? tip "ヒント3"

    multipartの場合は、`get_body(preferencelist=("plain",))` で本文パートを探せます。
    単純なメールでは、メッセージ自身が本文を持ちます。

??? tip "ヒント4"

    `get_content()` で本文を文字列として取り出し、最後に `strip()` で前後の空白を落とします。

