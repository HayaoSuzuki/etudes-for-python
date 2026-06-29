---
title: "052: 「同じ形の試験を並べる」のヒント"
description: "unittestとsubTestで複数の入力例をまとめて検査する。"
difficulty: 3
---

# 052: 「同じ形の試験を並べる」のヒント

[問題](../problems/052-unittest-table-cases.md) / [解答](../solutions/052-unittest-table-cases.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `make_slug` は、文字を1つずつ見て、残す文字と区切りに変える文字を分けると実装できます。

??? tip "ヒント2"

    ASCIIの英数字かどうかは、`ch.isascii()` と `ch.isalnum()` を組み合わせて判定できます。
    英字は `lower()` で小文字にします。

??? tip "ヒント3"

    区切り文字が連続したときにハイフンを何度も追加しないようにします。
    最後に `strip("-")` で先頭と末尾のハイフンを取り除けます。

??? tip "ヒント4"

    `unittest.TestCase` では、複数の入出力例をリストにしてループできます。
    各ケースを `with self.subTest(text=text):` の中で検査すると、どの入力で失敗したかがわかりやすくなります。

