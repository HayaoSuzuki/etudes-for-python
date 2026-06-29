---
title: "068: 「偽ならそのまま帰る」のヒント"
description: "andとorが真偽値ではなく評価された値を返すことを確かめる。"
difficulty: 3
---

# 068: 「偽ならそのまま帰る」のヒント

[問題](../problems/068-boolean-operands-return.md) / [解答](../solutions/068-boolean-operands-return.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `and` と `or` は、必ず `True` または `False` を返す演算子ではありません。

??? tip "ヒント2"

    `a or b`、`a and b`、`not a` をそのまま辞書に入れます。

??? tip "ヒント3"

    `not` は新しい真偽値を作るので、こちらは常に `bool` になります。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#boolean-operations)

