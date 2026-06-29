---
title: "099: 「並べ替えの鍵を取り出す」のヒント"
description: "operator.itemgetterで辞書の値を取り出し、複数条件で順位を並べる。"
difficulty: 3
---

# 099: 「並べ替えの鍵を取り出す」のヒント

[問題](../problems/099-operator-sort-key.md) / [解答](../solutions/099-operator-sort-key.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `sorted` は、元のリストを変更せず、新しいリストを返します。

??? tip "ヒント2"

    `itemgetter("score")` は、辞書から `score` の値を取り出す関数を作ります。
    `itemgetter("age", "name")` のように複数の値も取り出せます。

??? tip "ヒント3"

    点数だけは高い順なので、キーに入れるときに符号を反転します。
    年齢と名前はそのまま昇順にします。

??? tip "ヒント4"

    キー関数の中で、`(-score_getter(player), *age_name_getter(player))` のようなタプルを作ります。
    タプルは先頭から順に比較されます。
