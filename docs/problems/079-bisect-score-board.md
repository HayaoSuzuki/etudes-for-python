---
title: "079: 点数表に割り込む"
description: "bisectでソート済みの点数表に新しい記録を挿入する。"
difficulty: 3
---

# 079: 点数表に割り込む

[ヒント](../hints/079-bisect-score-board.md) / [解答](../solutions/079-bisect-score-board.md)

**難易度:** ☆☆☆

## 問題

関数 `insert_scoreboard(board, name, score)` を書いてください。

`board` は `(score, name)` のタプルのリストです。
点数の高い順に並んでおり、同点の場合は登録が早い順に並んでいます。

新しい記録を、点数表の正しい位置に挿入した新しいリストを返してください。

## 制約

- `bisect` モジュールを使ってください。
- `board` はすでに正しく並んでいるものとします。
- 同点の場合、新しい記録は同じ点数の記録の後ろに入れてください。
- 元の `board` は変更しないでください。

## 例

```python
>>> board = [(100, "Ann"), (90, "Bob"), (90, "Cid"), (70, "Dan")]
>>> insert_scoreboard(board, "Eve", 90)
[(100, 'Ann'), (90, 'Bob'), (90, 'Cid'), (90, 'Eve'), (70, 'Dan')]
>>> board
[(100, 'Ann'), (90, 'Bob'), (90, 'Cid'), (70, 'Dan')]
>>> insert_scoreboard(board, "Fin", 95)
[(100, 'Ann'), (95, 'Fin'), (90, 'Bob'), (90, 'Cid'), (70, 'Dan')]
```

## 発展

挿入後に上位 `n` 件だけを残す関数に拡張してください。

## 参考

- [bisect](https://docs.python.org/ja/3.14/library/bisect.html)
