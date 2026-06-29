---
title: "011: 「カンマの向こうに点がある」のヒント"
description: "カンマ区切りの文字列から、整数のリストを作る。"
difficulty: 2
---

# 011: 「カンマの向こうに点がある」のヒント

[問題](../problems/011-comma-separated-scores.md) / [解答](../solutions/011-comma-separated-scores.md)

**難易度:** ☆☆

??? tip "ヒント1"

    空文字列は、先に特別扱いすると考えやすくなります。

??? tip "ヒント2"

    文字列は `split(",")` でカンマごとに分けられます。

??? tip "ヒント3"

    各項目に `strip()` を使ってから、`int()` で整数に変換します。
