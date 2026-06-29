---
title: "081: 「カウントダウンは何度でも始まる」のヒント"
description: "__iter__と__next__を実装し、再利用できるイテラブルと一度だけ進むイテレータを分ける。"
difficulty: 4
---

# 081: 「カウントダウンは何度でも始まる」のヒント

[問題](../problems/081-custom-iterator.md) / [解答](../solutions/081-custom-iterator.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `for` 文や `list()` は、まず対象の `__iter__()` を呼びます。
    返ってきたイテレータに対して、値がなくなるまで `__next__()` を呼びます。

??? tip "ヒント2"

    イテレータ自身の `__iter__()` は、普通は `self` を返します。
    これにより、イテレータを直接 `for` 文に渡せます。

??? tip "ヒント3"

    `Countdown` を何度でも反復できるようにするには、`Countdown` 自身に現在位置を持たせないほうが扱いやすくなります。
    現在位置は `CountdownIterator` 側に持たせます。

??? tip "ヒント4"

    `Countdown.__iter__()` は、毎回新しい `CountdownIterator` を作って返します。
    `CountdownIterator.__next__()` は、現在の値を返してから1つ減らし、0より小さくなったら `StopIteration` を送出します。
