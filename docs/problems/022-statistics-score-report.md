---
title: "022: 点数の分布を読む"
description: "statisticsで平均、中央値、母標準偏差を求める。"
difficulty: 3
---

# 022: 点数の分布を読む

[ヒント](../hints/022-statistics-score-report.md) / [解答](../solutions/022-statistics-score-report.md)

**難易度:** ☆☆☆

## 問題

関数 `score_report(scores)` を書いてください。

この関数は、点数のリストを受け取り、件数、平均、中央値、母標準偏差を持つ辞書を返します。

## 制約

- `statistics` モジュールを使ってください。
- `scores` は数値のリストです。
- 空のリストが渡された場合は `ValueError` を送出してください。
- 戻り値は、キー `count`、`mean`、`median`、`pstdev` を持つ辞書です。
- `mean`、`median`、`pstdev` は `float` として返してください。

## 例

```python
>>> score_report([80, 80, 100, 100])
{'count': 4, 'mean': 90.0, 'median': 90.0, 'pstdev': 10.0}
>>> score_report([100])
{'count': 1, 'mean': 100.0, 'median': 100.0, 'pstdev': 0.0}
```

## 発展

標本標準偏差も返すようにしてください。

## 参考

- [statistics](https://docs.python.org/ja/3.14/library/statistics.html)

