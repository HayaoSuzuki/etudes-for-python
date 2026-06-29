---
title: "099: 「並べ替えの鍵を取り出す」の解答"
description: "itemgetterで辞書の値を取り出し、タプルのキーで複数条件ソートする。"
difficulty: 3
---

# 099: 「並べ替えの鍵を取り出す」の解答

[問題](../problems/099-operator-sort-key.md) / [ヒント](../hints/099-operator-sort-key.md)

**難易度:** ☆☆☆

## 方針

点数は降順、年齢と名前は昇順です。
`sorted` のキーとして、`(-score, age, name)` のタプルを作ります。

値の取り出しには `itemgetter` を使います。

## 実装

```python
from operator import itemgetter


def rank_players(players):
    get_score = itemgetter("score")
    get_age_name = itemgetter("age", "name")

    return sorted(
        players,
        key=lambda player: (-get_score(player), *get_age_name(player)),
    )
```

## 確認

```python
players = [
    {"name": "Bob", "score": 90, "age": 20},
    {"name": "Ann", "score": 100, "age": 22},
    {"name": "Cid", "score": 90, "age": 18},
]

assert [player["name"] for player in rank_players(players)] == ["Ann", "Cid", "Bob"]
assert [player["name"] for player in players] == ["Bob", "Ann", "Cid"]
```

## 発展

`itemgetter` は辞書だけでなく、タプルやリストの要素取り出しにも使えます。
データ構造に合わせてキー関数を差し替えると、ソート条件を読みやすく保てます。

## 参考

- [operator](https://docs.python.org/ja/3.14/library/operator.html)
