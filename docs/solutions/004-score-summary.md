---
title: "004: 「足して割れば、だいたい人生」の解答"
description: "点数のリストから合計と平均を求める。"
difficulty: 1
---

# 004: 「足して割れば、だいたい人生」の解答

[問題](../problems/004-score-summary.md) / [ヒント](../hints/004-score-summary.md)

**難易度:** ☆

## 方針

平均は合計を個数で割って求めます。
ただし、空のリストでは個数が0なので、先に空かどうかを判定します。

## 実装

```python
def score_summary(scores):
    if scores == []:
        return (0, 0.0)

    total = sum(scores)
    average = total / len(scores)
    return (total, average)
```

## 確認

```python
assert score_summary([80, 90, 70]) == (240, 80.0)
assert score_summary([100]) == (100, 100.0)
assert score_summary([]) == (0, 0.0)
```

## 発展

小数第1位まで丸めるなら、返り値に `round(average, 1)` を使えます。
丸める前の値も必要なら、関数を分けてください。

