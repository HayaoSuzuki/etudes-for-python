---
title: "099: 並べ替えの鍵を取り出す"
description: "operator.itemgetterで辞書の値を取り出し、複数条件で順位を並べる。"
difficulty: 3
---

# 099: 並べ替えの鍵を取り出す

[ヒント](../hints/099-operator-sort-key.md) / [解答](../solutions/099-operator-sort-key.md)

**難易度:** ☆☆☆

## 問題

関数 `rank_players(players)` を書いてください。

`players` は、プレイヤーを表す辞書のリストです。
各辞書は `name`、`score`、`age` を持ちます。

点数の高い順、年齢の低い順、名前の昇順で並べた新しいリストを返してください。

## 制約

- `operator.itemgetter` を使ってください。
- 元の `players` は変更しないでください。
- 戻り値は、プレイヤー辞書の新しいリストです。
- 点数は整数、年齢は整数、名前は文字列です。

## 例

```python
>>> players = [
...     {"name": "Bob", "score": 90, "age": 20},
...     {"name": "Ann", "score": 100, "age": 22},
...     {"name": "Cid", "score": 90, "age": 18},
... ]
>>> [player["name"] for player in rank_players(players)]
['Ann', 'Cid', 'Bob']
```

## 発展

並べ替え条件を引数で切り替えられるようにしてください。

## 参考

- [operator](https://docs.python.org/ja/3.14/library/operator.html)
