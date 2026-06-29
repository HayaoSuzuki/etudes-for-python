---
title: "055: 「例外には親がいる」のヒント"
description: "raise fromで変換前の例外を__cause__として残す。"
difficulty: 4
---

# 055: 「例外には親がいる」のヒント

[問題](../problems/055-exception-cause.md) / [解答](../solutions/055-exception-cause.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    辞書から値を取り出す処理と、整数へ変換する処理を別々の `try` 文にします。

??? tip "ヒント2"

    `except KeyError as exc:` で元の例外を受け取り、新しい `KeyError` を `from exc` で送出します。

??? tip "ヒント3"

    `int()` の変換失敗では、`ValueError` または `TypeError` が起こりえます。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/simple_stmts.html#the-raise-statement)
