---
title: "035: 「42か、それ以外か」のヒント"
description: "文字列を整数へ変換し、失敗したらNoneを返す。"
difficulty: 2
---

# 035: 「42か、それ以外か」のヒント

[問題](../problems/035-int-or-none.md) / [解答](../solutions/035-int-or-none.md)

**難易度:** ☆☆

??? tip "ヒント1"

    `int(text)` は、変換できない文字列に対して `ValueError` を送出します。

??? tip "ヒント2"

    `try` と `except ValueError` を使うと、変換失敗を関数の中で処理できます。

??? tip "ヒント3"

    変換に成功したら整数を返し、失敗したら `None` を返します。
