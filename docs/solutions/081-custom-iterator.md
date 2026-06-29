---
title: "081: 「カウントダウンは何度でも始まる」の解答"
description: "再利用できるCountdownと一度だけ進むCountdownIteratorに責務を分ける。"
difficulty: 4
---

# 081: 「カウントダウンは何度でも始まる」の解答

[問題](../problems/081-custom-iterator.md) / [ヒント](../hints/081-custom-iterator.md)

**難易度:** ☆☆☆☆

## 方針

`Countdown` は何度でも反復できるイテラブルにします。
そのため、現在位置は `Countdown` ではなく、毎回作る `CountdownIterator` に持たせます。

`CountdownIterator` は `__iter__` で自分自身を返し、`__next__` で現在の値を返してから1つ減らします。
0を返したあとは、次の呼び出しで `StopIteration` を送出します。

## 実装

```python
class Countdown:
    def __init__(self, start):
        if start < 0:
            raise ValueError("start must be non-negative")
        self.start = start

    def __iter__(self):
        return CountdownIterator(self.start)


class CountdownIterator:
    def __init__(self, current):
        self.current = current

    def __iter__(self):
        return self

    def __next__(self):
        if self.current < 0:
            raise StopIteration
        value = self.current
        self.current -= 1
        return value
```

## 確認

```python
countdown = Countdown(3)

assert list(countdown) == [3, 2, 1, 0]
assert list(countdown) == [3, 2, 1, 0]

iterator = iter(countdown)
assert iter(iterator) is iterator
assert next(iterator) == 3
assert next(iterator) == 2

try:
    Countdown(-1)
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

`range` のように、開始値、終了値、増減幅を指定できるクラスに拡張すると、停止条件の設計が少し難しくなります。
その場合も、反復可能な本体と現在位置を持つイテレータを分けると考えやすくなります。

## 参考

- [イテレータ型](https://docs.python.org/ja/3.14/library/stdtypes.html#iterator-types)
