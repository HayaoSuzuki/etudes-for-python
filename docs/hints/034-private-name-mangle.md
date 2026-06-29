---
title: "034: 「二本の下線は名前を隠す」のヒント"
description: "private name manglingの規則を関数として実装する。"
difficulty: 5
---

# 034: 「二本の下線は名前を隠す」のヒント

[問題](../problems/034-private-name-mangle.md) / [解答](../solutions/034-private-name-mangle.md)

**難易度:** ☆☆☆☆☆

??? tip "ヒント1"

    まず、`identifier` が2個以上の `_` で始まるかを調べます。

??? tip "ヒント2"

    次に、2個以上の `_` で終わる名前を対象外にします。

??? tip "ヒント3"

    `class_name.lstrip("_")` で、クラス名の先頭の `_` を取り除けます。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#private-name-mangling)
