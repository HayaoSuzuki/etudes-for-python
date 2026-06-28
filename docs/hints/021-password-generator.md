---
title: "021: 「世界の合言葉は森」のヒント"
description: "secretsで候補を作り、正規表現で検査する。"
---

# 021: 「世界の合言葉は森」のヒント

[問題](../problems/021-password-generator.md) / [解答](../solutions/021-password-generator.md)

??? tip "ヒント1"

    文字の候補は、`string.ascii_letters`、`string.digits`、記号の文字列を連結して作れます。
    1文字選ぶときは `secrets.choice` を使います。

??? tip "ヒント2"

    条件を満たすかどうかを調べる関数を別に作ると、生成部分が単純になります。
    前の2問と同じように、`fullmatch` と `search` を使えます。

??? tip "ヒント3"

    ランダムに作った候補が条件を満たすとは限りません。
    候補を作り、検査し、失敗したらもう一度作る、という流れにします。

??? tip "ヒント4"

    `length < 8` は、候補を作る前に `ValueError` にします。
    生成された文字列の長さは、`len(password) == length` で確認できます。
