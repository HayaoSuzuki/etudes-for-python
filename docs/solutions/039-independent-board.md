---
title: "039: 「昨日と同じリストではない」の解答"
description: "行どうしが共有されない二次元リストを作る。"
difficulty: 3
---

# 039: 「昨日と同じリストではない」の解答

[問題](../problems/039-independent-board.md) / [ヒント](../hints/039-independent-board.md)

**難易度:** ☆☆☆

## 方針

行を作る処理を、行数ぶん繰り返します。
各行を作るたびに新しいリストを用意することで、行どうしが同じリストを共有しないようにします。

## 実装

```python
def make_board(rows, columns, fill=None):
    board = []
    for _ in range(rows):
        row = []
        for _ in range(columns):
            row.append(fill)
        board.append(row)
    return board
```

## 確認

```python
assert make_board(2, 3, 0) == [[0, 0, 0], [0, 0, 0]]
board = make_board(2, 3, 0)
board[0][0] = 9
assert board == [[9, 0, 0], [0, 0, 0]]
assert make_board(0, 3) == []
```

## 発展

`[[fill] * columns] * rows` は、同じ行リストへの参照を複数並べます。
そのため、1行だけ変更したつもりでも、ほかの行まで変わります。
