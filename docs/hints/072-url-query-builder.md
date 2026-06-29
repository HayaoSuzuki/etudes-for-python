---
title: "072: 「URLはクエリを背負って走る」のヒント"
description: "urllib.parseでURLとクエリ文字列を組み立てる。"
difficulty: 2
---

# 072: 「URLはクエリを背負って走る」のヒント

[問題](../problems/072-url-query-builder.md) / [解答](../solutions/072-url-query-builder.md)

**難易度:** ☆☆

??? tip "ヒント1"

    `urljoin(base, path)` を使うと、基底URLと相対パスを結合できます。

??? tip "ヒント2"

    クエリ文字列は `urlencode(params)` で作れます。

??? tip "ヒント3"

    値がリストのパラメータを複数回出したい場合は、`urlencode(params, doseq=True)` を使います。

??? tip "ヒント4"

    `params` が空のときは、クエリ文字列を作らずURLだけを返します。
