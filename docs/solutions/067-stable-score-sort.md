---
title: "067: 「同点の列は昨日を覚えている」の解答"
description: "sortedのkeyと安定ソートを使って、複数条件で順位を並べる。"
difficulty: 3
---

# 067: 「同点の列は昨日を覚えている」の解答

[問題](../problems/067-stable-score-sort.md) / [ヒント](../hints/067-stable-score-sort.md)

**難易度:** ☆☆☆

## 方針

得点の降順は `-entry["score"]` で表します。
提出時刻は小さいほど上位なので、そのままキーに入れます。
同じキーを持つ要素は、安定ソートによって元の順序に残ります。

## 実装

```python
def rank_scores(entries):
    ranked = sorted(
        entries,
        key=lambda entry: (-entry["score"], entry["submitted_at"]),
    )
    return [entry["name"] for entry in ranked]
```

## 確認

```python
entries = [
    {"name": "mika", "score": 90, "submitted_at": 12},
    {"name": "jun", "score": 90, "submitted_at": 9},
    {"name": "ao", "score": 80, "submitted_at": 4},
    {"name": "ren", "score": 90, "submitted_at": 12},
]

assert rank_scores(entries) == ["jun", "mika", "ren", "ao"]
assert entries[0]["name"] == "mika"
```

## 発展

順位番号も返すようにしてください。
同じ `score` と `submitted_at` の人に同じ順位を与えるかどうかで、実装がどう変わるか確認してください。

## 参考

- [ソートのテクニック](https://docs.python.org/ja/3.14/howto/sorting.html)
