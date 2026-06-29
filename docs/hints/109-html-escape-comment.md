---
title: "109: 「コメントはそのままHTMLにしない」のヒント"
description: "html.escapeでユーザー入力をエスケープし、HTML断片を作る。"
difficulty: 3
---

# 109: 「コメントはそのままHTMLにしない」のヒント

[問題](../problems/109-html-escape-comment.md) / [解答](../solutions/109-html-escape-comment.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    ユーザー入力をHTMLに埋め込むときは、`<` や `&` などをそのまま出さないようにします。

??? tip "ヒント2"

    `html.escape(text, quote=True)` は、HTML上で特別な意味を持つ文字をエスケープします。
    `quote=True` なら引用符も対象になります。

??? tip "ヒント3"

    投稿者名と本文の両方を別々にエスケープします。

??? tip "ヒント4"

    エスケープ済みの値を使って、`<p><strong>{author}</strong>: {text}</p>` の形に組み立てます。
