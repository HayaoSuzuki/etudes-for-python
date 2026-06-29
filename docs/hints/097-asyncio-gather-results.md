---
title: "097: 「非同期の結果を順に集める」のヒント"
description: "asyncio.gatherで複数の非同期処理を実行し、入力順に結果を返す。"
difficulty: 4
---

# 097: 「非同期の結果を順に集める」のヒント

[問題](../problems/097-asyncio-gather-results.md) / [解答](../solutions/097-asyncio-gather-results.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `async def` で定義した関数の中では、`await` を使って非同期処理の結果を待てます。

??? tip "ヒント2"

    `jobs` の各要素は、呼び出すと await 可能な値を返す関数です。
    まず各ジョブを呼び出して、await 可能な値のリストを作ります。

??? tip "ヒント3"

    `asyncio.gather(*awaitables)` は、複数の await 可能な値をまとめて待ちます。
    結果の順序は、渡した順序と同じです。

??? tip "ヒント4"

    `gather` の戻り値はタプルではなくリストにそろえて返すと、問題の仕様と一致します。
    `list(await asyncio.gather(...))` の形にできます。
