---
title: "052: 「caseは形を見ている」のヒント"
description: "構造的パターンマッチで辞書、シーケンス、ガードを使い分ける。"
difficulty: 4
---

# 052: 「caseは形を見ている」のヒント

[問題](../problems/052-match-event.md) / [解答](../solutions/052-match-event.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    辞書の形は、マッピングパターンで判定できます。

??? tip "ヒント2"

    `int(x)` のようなクラスパターンを使うと、整数だけにマッチさせて値を束縛できます。

??? tip "ヒント3"

    `case ["resize", int(width), int(height)] if width > 0 and height > 0:` のように、ガードを追加できます。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/compound_stmts.html#the-match-statement)
