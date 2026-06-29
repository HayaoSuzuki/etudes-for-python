---
title: "100: 道順は覚えて数える"
description: "functools.cacheで再帰的な格子経路数の重複計算を避ける。"
difficulty: 4
---

# 100: 道順は覚えて数える

[ヒント](../hints/100-functools-cache-recursive.md) / [解答](../solutions/100-functools-cache-recursive.md)

**難易度:** ☆☆☆☆

## 問題

関数 `count_paths(width, height)` を書いてください。

左下から右上へ、右または上に1マスずつ進むとします。
横に `width` 回、縦に `height` 回進む必要があるとき、到達する道順の数を返してください。

## 制約

- `functools.cache` を使ってください。
- `width` と `height` は0以上の整数です。
- どちらかが負の場合は `ValueError` を送出してください。
- `width == 0` または `height == 0` の場合、道順は1通りです。
- `count_paths(20, 20)` を現実的な時間で計算できるようにしてください。

## 例

```python
>>> count_paths(2, 2)
6
>>> count_paths(3, 2)
10
>>> count_paths(0, 5)
1
```

## 発展

障害物があるマスを通れない場合にも対応してください。

## 参考

- [functools.cache](https://docs.python.org/ja/3.14/library/functools.html#functools.cache)
