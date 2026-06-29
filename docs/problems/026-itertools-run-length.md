---
title: "026: 同じ値はまとめて走る"
description: "itertools.groupbyで連続する同じ値をランレングス符号化する。"
difficulty: 3
---

# 026: 同じ値はまとめて走る

[ヒント](../hints/026-itertools-run-length.md) / [解答](../solutions/026-itertools-run-length.md)

**難易度:** ☆☆☆

## 問題

関数 `encode_runs(items)` と `decode_runs(runs)` を書いてください。

`encode_runs` は、連続する同じ値を `(value, count)` の形にまとめます。
`decode_runs` は、その結果から元のリストを復元します。

## 制約

- `encode_runs` では `itertools.groupby` を使ってください。
- `items` は任意のイテラブルです。
- `encode_runs` の戻り値はリストです。
- `decode_runs` の戻り値はリストです。
- `count` が0以下の要素を `decode_runs` に渡した場合は `ValueError` を送出してください。

## 例

```python
>>> encode_runs("aaabbcaaa")
[('a', 3), ('b', 2), ('c', 1), ('a', 3)]
>>> decode_runs([('a', 3), ('b', 2), ('c', 1), ('a', 3)])
['a', 'a', 'a', 'b', 'b', 'c', 'a', 'a', 'a']
>>> encode_runs([])
[]
```

## 発展

`decode_runs` をジェネレータにして、大きなデータでも少しずつ復元できるようにしてください。

## 参考

- [itertools.groupby](https://docs.python.org/ja/3.14/library/itertools.html#itertools.groupby)

