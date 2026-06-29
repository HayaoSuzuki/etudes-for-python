---
title: "024: 「よく出る言葉から並べる」のヒント"
description: "collections.Counterで単語の出現回数を数え、頻度順に上位語を返す。"
difficulty: 3
---

# 024: 「よく出る言葉から並べる」のヒント

[問題](../problems/024-counter-top-words.md) / [解答](../solutions/024-counter-top-words.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    最初に、文章から単語だけを取り出します。
    大文字小文字を区別しないので、数える前に小文字へそろえます。

??? tip "ヒント2"

    単語の抽出には正規表現が使えます。
    英数字とアポストロフィの連続を1単語として取り出します。

??? tip "ヒント3"

    `Counter` に単語のリストを渡すと、単語ごとの出現回数を数えられます。
    `stop_words` は同じく小文字へそろえてから除外します。

??? tip "ヒント4"

    並び順は、回数の降順、単語の昇順です。
    `sorted(counter.items(), key=lambda item: (-item[1], item[0]))` の形にすると指定できます。

