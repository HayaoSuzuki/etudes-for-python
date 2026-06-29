---
title: "033: 「例外の束をほどく」のヒント"
description: "except*でExceptionGroupを型ごとの部分グループに分ける。"
difficulty: 5
---

# 033: 「例外の束をほどく」のヒント

[問題](../problems/033-exception-group-count.md) / [解答](../solutions/033-exception-group-count.md)

**難易度:** ☆☆☆☆☆

??? tip "ヒント1"

    `except*` は、`ExceptionGroup` の中身を型に応じて部分グループに分けます。

??? tip "ヒント2"

    `except* ValueError as group:` の `group.exceptions` には、対応する例外だけが入ります。

??? tip "ヒント3"

    `except*` 節の中では `return` が使えないので、外側の辞書に個数を記録して最後に返します。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/compound_stmts.html#except-star)
