---
title: "039: 昨日と同じリストではない"
description: "行どうしが共有されない二次元リストを作る。"
difficulty: 3
---

# 039: 昨日と同じリストではない

[ヒント](../hints/039-independent-board.md) / [解答](../solutions/039-independent-board.md)

**難易度:** ☆☆☆

## 問題

関数 `make_board(rows, columns, fill=None)` を書いてください。
この関数は、`rows` 行 `columns` 列の二次元リストを返します。
各マスの初期値は `fill` とします。

返す二次元リストでは、ある行を変更しても、別の行が同時に変わってはいけません。

## 制約

- `rows` と `columns` は0以上の整数です。
- `rows` が0の場合は空のリストを返します。
- 各行は別々のリストにしてください。

## 例

```python
>>> make_board(2, 3, 0)
[[0, 0, 0], [0, 0, 0]]
>>> board = make_board(2, 3, 0)
>>> board[0][0] = 9
>>> board
[[9, 0, 0], [0, 0, 0]]
>>> make_board(0, 3)
[]
```

## 発展

`[[fill] * columns] * rows` で作ると何が起きるか、実際に試してください。
