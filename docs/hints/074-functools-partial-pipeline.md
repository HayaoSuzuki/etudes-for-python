---
title: "074: 「設定済みの整形関数を作る」のヒント"
description: "functools.partialで引数を固定した文字列整形関数を作る。"
difficulty: 3
---

# 074: 「設定済みの整形関数を作る」のヒント

[問題](../problems/074-functools-partial-pipeline.md) / [解答](../solutions/074-functools-partial-pipeline.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `format_message` は、本文を変換し、前後の文字列を付けるだけの関数です。

??? tip "ヒント2"

    `uppercase` が真なら、本文に `upper()` を適用します。
    そのあと `prefix + body + suffix` の形で組み立てます。

??? tip "ヒント3"

    `partial(function, keyword=value)` は、指定した引数を固定した新しい呼び出し可能オブジェクトを作ります。

??? tip "ヒント4"

    `make_formatter` では、`format_message` の `prefix`、`suffix`、`uppercase` を固定します。
    `text` はあとから渡せるように残します。

