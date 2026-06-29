---
title: "093: 「型ごとに表示を切り替える」のヒント"
description: "functools.singledispatchで値の型に応じた表示文字列を作る。"
difficulty: 4
---

# 093: 「型ごとに表示を切り替える」のヒント

[問題](../problems/093-singledispatch-format.md) / [解答](../solutions/093-singledispatch-format.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `@singledispatch` を付けた関数は、第一引数の型に応じて別の実装を呼び出せます。
    最初に書く関数は、未登録の型に対する既定の実装になります。

??? tip "ヒント2"

    型ごとの処理は、`@format_value.register` を付けた関数として追加できます。
    引数の型ヒントから登録する型を読み取れます。

??? tip "ヒント3"

    `bool` は `int` のサブクラスですが、`singledispatch` ではより具体的な型の実装が選ばれます。
    `bool` 用の実装を別に登録してください。

??? tip "ヒント4"

    リストの整形では、要素ごとにもう一度 `format_value` を呼びます。
    これにより、入れ子のリストや文字列、真偽値も同じ規則で整形できます。
