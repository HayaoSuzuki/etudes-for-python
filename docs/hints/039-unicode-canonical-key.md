---
title: "039: 「同じ顔をした別の文字」のヒント"
description: "Unicode正規化とcasefoldで、表記ゆれを比較用キーに変換する。"
difficulty: 3
---

# 039: 「同じ顔をした別の文字」のヒント

[問題](../problems/039-unicode-canonical-key.md) / [解答](../solutions/039-unicode-canonical-key.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    Unicodeでは、見た目が似ていても別の符号位置の文字があります。
    比較用の文字列を作ってから比べると扱いやすくなります。

??? tip "ヒント2"

    `unicodedata.normalize("NFKC", text)` は、互換文字を標準的な形に寄せます。

??? tip "ヒント3"

    `lower` よりも `casefold` のほうが、大小文字の比較用キーには向いています。

??? tip "ヒント4"

    重複除去では、見たキーを `set` に入れておきます。
    結果に入れるのは、正規化後の文字列ではなく元の文字列です。

