---
title: "050: 「inは古い扉も叩く」の解答"
description: "__contains__も__iter__もないオブジェクトでmembership testを成立させる。"
difficulty: 4
---

# 050: 「inは古い扉も叩く」の解答

[問題](../problems/050-getitem-membership.md) / [ヒント](../hints/050-getitem-membership.md)

**難易度:** ☆☆☆☆

## 方針

`__getitem__` だけを実装します。
`in` は、`__contains__` と `__iter__` がない場合、0から始まる整数添字で `__getitem__` を呼び出します。
範囲外では `IndexError` を送出して、探索を終わらせます。

## 実装

```python
class SquaresBelow:
    def __init__(self, limit):
        self.limit = limit

    def __getitem__(self, index):
        if not isinstance(index, int):
            raise TypeError("index must be an integer")
        if index < 0 or index >= self.limit:
            raise IndexError("index out of range")
        return index ** 2
```

## 確認

```python
squares = SquaresBelow(5)
assert squares[3] == 9
assert (16 in squares) is True
assert (25 in squares) is False
assert list(squares) == [0, 1, 4, 9, 16]
```

## 発展

`__contains__` を追加すると、`in` の判定を探索ではなく計算で行えます。
平方数かどうかを調べる実装に変えてください。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#membership-test-operations)
