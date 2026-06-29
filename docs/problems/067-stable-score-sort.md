---
title: "067: 同点の列は昨日を覚えている"
description: "sortedで複数条件の順位を並べる。"
difficulty: 3
---

# 067: 同点の列は昨日を覚えている

[ヒント](../hints/067-stable-score-sort.md) / [解答](../solutions/067-stable-score-sort.md)

**難易度:** ☆☆☆

## 問題

関数 `rank_scores(entries)` を書いてください。
この関数は、得点表を順位順に並べ、名前のリストを返します。

各要素は、キー `name`、`score`、`submitted_at` を持つ辞書です。
`submitted_at` は提出時刻を分で表した整数です。

順位は次の規則で決めます。

- `score` が高いほど上位
- `score` が同じなら、`submitted_at` が小さいほど上位
- `score` と `submitted_at` が同じなら、元の順序を保つ

## 制約

- `sorted` を使ってください。
- 元のリストと辞書を書き換えないでください。
- 戻り値は名前のリストです。

## 例

```python
>>> entries = [
...     {"name": "mika", "score": 90, "submitted_at": 12},
...     {"name": "jun", "score": 90, "submitted_at": 9},
...     {"name": "ao", "score": 80, "submitted_at": 4},
...     {"name": "ren", "score": 90, "submitted_at": 12},
... ]
>>> rank_scores(entries)
['jun', 'mika', 'ren', 'ao']
```

## 参考

- [ソートのテクニック](https://docs.python.org/ja/3.14/howto/sorting.html)
