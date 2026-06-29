---
title: "069: 「真ん中は一度だけ呼ばれる」のヒント"
description: "比較の連鎖で中央の式が一度だけ評価されることを使う。"
difficulty: 3
---

# 069: 「真ん中は一度だけ呼ばれる」のヒント

[問題](../problems/069-comparison-chain-once.md) / [解答](../solutions/069-comparison-chain-once.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    Pythonでは、比較を連鎖して書けます。

??? tip "ヒント2"

    `low < get_value() <= high` と書いた場合、中央の式は一度だけ評価されます。

??? tip "ヒント3"

    `low < get_value() and get_value() <= high` と書くと、条件によっては2回呼び出してしまいます。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#comparisons)

