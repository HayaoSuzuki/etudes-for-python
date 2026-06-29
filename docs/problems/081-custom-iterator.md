---
title: "081: カウントダウンは何度でも始まる"
description: "__iter__と__next__を実装し、再利用できるイテラブルと一度だけ進むイテレータを分ける。"
difficulty: 4
---

# 081: カウントダウンは何度でも始まる

[ヒント](../hints/081-custom-iterator.md) / [解答](../solutions/081-custom-iterator.md)

**難易度:** ☆☆☆☆

## 問題

`Countdown` と `CountdownIterator` を書いてください。

`Countdown(start)` は、`start` から `0` までの整数を順に返すイテラブルです。
同じ `Countdown` オブジェクトは、何度でも最初から反復できるようにしてください。

`CountdownIterator` は、実際に値を1つずつ返すイテレータです。

## 制約

- `yield` を使わず、`__iter__` と `__next__` を実装してください。
- `start` は0以上の整数です。
- `start` が負の場合は `ValueError` を送出してください。
- `Countdown.__iter__()` は、新しい `CountdownIterator` を返してください。
- `CountdownIterator.__iter__()` は、自分自身を返してください。
- 次の値がなくなったら `StopIteration` を送出してください。

## 例

```python
>>> countdown = Countdown(3)
>>> list(countdown)
[3, 2, 1, 0]
>>> list(countdown)
[3, 2, 1, 0]
>>> iterator = iter(countdown)
>>> iter(iterator) is iterator
True
>>> next(iterator)
3
>>> next(iterator)
2
```

## 発展

終了値も指定できる `Countdown(start, stop)` に拡張してください。

## 参考

- [イテレータ型](https://docs.python.org/ja/3.14/library/stdtypes.html#iterator-types)
