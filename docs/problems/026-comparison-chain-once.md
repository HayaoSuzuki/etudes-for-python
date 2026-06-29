---
title: "026: 真ん中は一度だけ呼ばれる"
description: "比較の連鎖で中央の式が一度だけ評価されることを使う。"
difficulty: 3
---

# 026: 真ん中は一度だけ呼ばれる

[ヒント](../hints/026-comparison-chain-once.md) / [解答](../solutions/026-comparison-chain-once.md)

**難易度:** ☆☆☆

## 問題

関数 `between_once(get_value, low, high)` を書いてください。
この関数は、`get_value()` が返す値 `value` について、`low < value <= high` が成り立つかを返します。

`get_value()` は、必ず1回だけ呼び出してください。
比較のために同じ値を2回取得してはいけません。

## 制約

- `get_value` は引数なしの関数です。
- `get_value()` の返り値、`low`、`high` は比較可能です。
- 返り値は `bool` です。

## 例

```python
>>> calls = []
>>> def read_value():
...     calls.append("called")
...     return 5
>>> between_once(read_value, 1, 5)
True
>>> calls
['called']
>>> between_once(lambda: 0, 1, 5)
False
```

## 参考

- [比較](https://docs.python.org/ja/3.14/reference/expressions.html#comparisons)
