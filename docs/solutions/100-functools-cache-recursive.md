---
title: "100: 「道順は覚えて数える」の解答"
description: "cacheを付けた再帰関数で格子経路数を一度ずつ計算する。"
difficulty: 4
---

# 100: 「道順は覚えて数える」の解答

[問題](../problems/100-functools-cache-recursive.md) / [ヒント](../hints/100-functools-cache-recursive.md)

**難易度:** ☆☆☆☆

## 方針

最後の1歩は、左から来るか下から来るかのどちらかです。
したがって、`paths(w, h) = paths(w - 1, h) + paths(w, h - 1)` と書けます。

同じ引数の組を何度も計算しないように、内側の再帰関数に `cache` を付けます。

## 実装

```python
from functools import cache


def count_paths(width, height):
    if width < 0 or height < 0:
        raise ValueError("width and height must be non-negative")

    @cache
    def paths(w, h):
        if w == 0 or h == 0:
            return 1
        return paths(w - 1, h) + paths(w, h - 1)

    return paths(width, height)
```

## 確認

```python
assert count_paths(2, 2) == 6
assert count_paths(3, 2) == 10
assert count_paths(0, 5) == 1
assert count_paths(20, 20) == 137846528820

try:
    count_paths(-1, 2)
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

この問題は組み合わせでも解けます。
右へ進む回数と上へ進む回数の並べ方なので、合計 `width + height` 回のうち `width` 回を選ぶ数になります。

## 参考

- [functools.cache](https://docs.python.org/ja/3.14/library/functools.html#functools.cache)
