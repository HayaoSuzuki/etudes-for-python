---
title: "098: 「点数の分布を読む」の解答"
description: "statisticsの関数で件数、平均、中央値、母標準偏差をまとめる。"
difficulty: 3
---

# 098: 「点数の分布を読む」の解答

[問題](../problems/098-statistics-score-report.md) / [ヒント](../hints/098-statistics-score-report.md)

**難易度:** ☆☆☆

## 方針

空の入力では統計量を計算できないため、先に拒否します。
平均、中央値、母標準偏差は `statistics` の関数で求められます。

戻り値の型をそろえるため、統計量は `float` に変換します。

## 実装

```python
import statistics


def score_report(scores):
    if not scores:
        raise ValueError("scores must not be empty")

    return {
        "count": len(scores),
        "mean": float(statistics.mean(scores)),
        "median": float(statistics.median(scores)),
        "pstdev": float(statistics.pstdev(scores)),
    }
```

## 確認

```python
assert score_report([80, 80, 100, 100]) == {
    "count": 4,
    "mean": 90.0,
    "median": 90.0,
    "pstdev": 10.0,
}
assert score_report([100]) == {
    "count": 1,
    "mean": 100.0,
    "median": 100.0,
    "pstdev": 0.0,
}

try:
    score_report([])
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

標本標準偏差は `statistics.stdev` で求められます。
ただし、要素数が1つだけの場合は標本標準偏差を計算できないため、その場合の仕様を決める必要があります。

## 参考

- [statistics](https://docs.python.org/ja/3.14/library/statistics.html)
