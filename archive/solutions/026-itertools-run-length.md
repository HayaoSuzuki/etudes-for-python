---
title: "026: 「同じ値はまとめて走る」の解答"
description: "groupbyで連続する同じ値をまとめ、値と個数の組へ変換する。"
difficulty: 3
---

# 026: 「同じ値はまとめて走る」の解答

[問題](../problems/026-itertools-run-length.md) / [ヒント](../hints/026-itertools-run-length.md)

**難易度:** ☆☆☆

## 方針

`groupby` は、連続する同じ値ごとにグループを作ります。
各グループの長さを数えれば、`(value, count)` の形にできます。

復元では、各組に対して値を `count` 回だけ結果リストに追加します。

## 実装

```python
from itertools import groupby


def encode_runs(items):
    return [
        (value, sum(1 for _ in group))
        for value, group in groupby(items)
    ]


def decode_runs(runs):
    result = []
    for value, count in runs:
        if count <= 0:
            raise ValueError("count must be positive")
        result.extend([value] * count)
    return result
```

## 確認

```python
assert encode_runs("aaabbcaaa") == [
    ("a", 3),
    ("b", 2),
    ("c", 1),
    ("a", 3),
]
assert decode_runs([("a", 3), ("b", 2), ("c", 1), ("a", 3)]) == [
    "a",
    "a",
    "a",
    "b",
    "b",
    "c",
    "a",
    "a",
    "a",
]
assert encode_runs([]) == []

try:
    decode_runs([("x", 0)])
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

`groupby` は隣り合う値だけをまとめます。
値全体の頻度を数える用途では、`Counter` など別の道具を使います。

## 参考

- [itertools.groupby](https://docs.python.org/ja/3.14/library/itertools.html#itertools.groupby)

