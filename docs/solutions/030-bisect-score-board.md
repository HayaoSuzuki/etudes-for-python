---
title: "030: 「点数表に割り込む」の解答"
description: "点数にマイナスを付けたキー列にbisect_rightを使い、同点の後ろへ挿入する。"
difficulty: 3
---

# 030: 「点数表に割り込む」の解答

[問題](../problems/030-bisect-score-board.md) / [ヒント](../hints/030-bisect-score-board.md)

**難易度:** ☆☆☆

## 方針

`bisect` は昇順の列に対して使います。
点数表は高い点数が前に来る降順なので、点数にマイナスを付けたキー列を作ります。

同点の記録の後ろへ入れるため、`bisect_right` で右側の挿入位置を求めます。

## 実装

```python
from bisect import bisect_right


def insert_scoreboard(board, name, score):
    keys = [-entry_score for entry_score, _ in board]
    index = bisect_right(keys, -score)
    return board[:index] + [(score, name)] + board[index:]
```

## 確認

```python
board = [(100, "Ann"), (90, "Bob"), (90, "Cid"), (70, "Dan")]

assert insert_scoreboard(board, "Eve", 90) == [
    (100, "Ann"),
    (90, "Bob"),
    (90, "Cid"),
    (90, "Eve"),
    (70, "Dan"),
]
assert board == [(100, "Ann"), (90, "Bob"), (90, "Cid"), (70, "Dan")]
assert insert_scoreboard(board, "Fin", 95) == [
    (100, "Ann"),
    (95, "Fin"),
    (90, "Bob"),
    (90, "Cid"),
    (70, "Dan"),
]
```

## 発展

`board` が非常に大きい場合、キー列を毎回作るとそのぶんの時間がかかります。
頻繁に挿入するなら、検索用のキー列もあわせて保持する設計を検討します。

## 参考

- [bisect](https://docs.python.org/ja/3.14/library/bisect.html)

