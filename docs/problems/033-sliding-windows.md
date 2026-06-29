---
title: "033: 窓は一歩ずつ流れていく"
description: "イテレータを使って、連続する固定長の窓を生成する。"
difficulty: 4
---

# 033: 窓は一歩ずつ流れていく

[ヒント](../hints/033-sliding-windows.md) / [解答](../solutions/033-sliding-windows.md)

**難易度:** ☆☆☆☆

## 問題

関数 `sliding_windows(iterable, size)` と `moving_average(values, size)` を書いてください。

`sliding_windows` は、任意のイテラブルから、連続する長さ `size` のタプルを順に生成します。
`moving_average` は、その窓ごとの平均値をリストで返します。

## 制約

- `sliding_windows` はジェネレータとして実装してください。
- 入力全体をリストに変換しないでください。
- `size` が0以下なら `ValueError` を送出してください。
- 要素数が `size` 未満なら、窓は一つも生成しません。

## 例

```python
>>> list(sliding_windows([1, 2, 3, 4], 3))
[(1, 2, 3), (2, 3, 4)]
>>> moving_average([10, 20, 30, 40], 2)
[15.0, 25.0, 35.0]
>>> list(sliding_windows((n * n for n in range(5)), 2))
[(0, 1), (1, 4), (4, 9), (9, 16)]
```

## 参考

- [関数型プログラミング HOWTO](https://docs.python.org/ja/3.14/howto/functional.html)

