---
title: "051: 「出口で例外を見分ける」のヒント"
description: "__exit__の返り値で特定の例外だけを抑制する。"
difficulty: 4
---

# 051: 「出口で例外を見分ける」のヒント

[問題](../problems/051-suppress-only.md) / [解答](../solutions/051-suppress-only.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `__exit__` には、例外型、例外オブジェクト、トレースバックが渡されます。

??? tip "ヒント2"

    `__exit__` が真と解釈される値を返すと、例外は抑制されます。

??? tip "ヒント3"

    `exc_type is not None and issubclass(exc_type, self.exception_type)` で対象の例外かどうかを判定できます。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/compound_stmts.html#the-with-statement)
