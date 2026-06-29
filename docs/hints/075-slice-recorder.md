---
title: "075: 「スライスは切らずに渡される」のヒント"
description: "__getitem__に渡されるsliceオブジェクトとタプル添字を観察する。"
difficulty: 4
---

# 075: 「スライスは切らずに渡される」のヒント

[問題](../problems/075-slice-recorder.md) / [解答](../solutions/075-slice-recorder.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    スライス式は、`__getitem__` に渡される前に `slice` オブジェクトになります。

??? tip "ヒント2"

    カンマ区切りの添字は、タプルとして渡されます。

??? tip "ヒント3"

    `isinstance(key, slice)` と `isinstance(key, tuple)` で場合分けできます。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#slicings)

