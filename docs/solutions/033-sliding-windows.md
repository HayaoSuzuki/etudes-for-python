---
title: "033: 「窓は一歩ずつ流れていく」の解答"
description: "イテレータとdequeを使って、連続する固定長の窓を生成する。"
difficulty: 4
---

# 033: 「窓は一歩ずつ流れていく」の解答

[問題](../problems/033-sliding-windows.md) / [ヒント](../hints/033-sliding-windows.md)

**難易度:** ☆☆☆☆

## 方針

入力をイテレータにし、最初の窓だけ先に作ります。
その後は新しい要素を一つ読むたびに窓を更新して、タプルとして返します。

## 実装

```python
from collections import deque


def sliding_windows(iterable, size):
    if size <= 0:
        raise ValueError("size must be positive")

    iterator = iter(iterable)
    window = deque(maxlen=size)

    for _ in range(size):
        try:
            window.append(next(iterator))
        except StopIteration:
            return

    yield tuple(window)

    for item in iterator:
        window.append(item)
        yield tuple(window)


def moving_average(values, size):
    return [
        sum(window) / size
        for window in sliding_windows(values, size)
    ]
```

## 確認

```python
assert list(sliding_windows([1, 2, 3, 4], 3)) == [(1, 2, 3), (2, 3, 4)]
assert moving_average([10, 20, 30, 40], 2) == [15.0, 25.0, 35.0]
assert list(sliding_windows((n * n for n in range(5)), 2)) == [
    (0, 1),
    (1, 4),
    (4, 9),
    (9, 16),
]
assert list(sliding_windows([1], 2)) == []
```

## 発展

`moving_average` は窓ごとに `sum` を計算しているため、窓が大きいと無駄が増えます。
直前の合計を更新する形に変えてください。

## 参考

- [関数型プログラミング HOWTO](https://docs.python.org/ja/3.14/howto/functional.html)

