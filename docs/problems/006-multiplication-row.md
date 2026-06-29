---
title: "006: 九つの積の物語"
description: "九九のうち、ある段の一行を作る。"
difficulty: 1
---

# 006: 九つの積の物語

[ヒント](../hints/006-multiplication-row.md) / [解答](../solutions/006-multiplication-row.md)

**難易度:** ☆

## 問題

関数 `multiplication_row(n)` を書いてください。
この関数は、整数 `n` を受け取り、`n * 1` から `n * 9` までの結果を並べたリストを返します。

## 制約

- `n` は1以上9以下の整数です。
- 戻り値は長さ9の整数リストです。

## 例

```python
>>> multiplication_row(3)
[3, 6, 9, 12, 15, 18, 21, 24, 27]
>>> multiplication_row(9)[-1]
81
>>> multiplication_row(1)
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## 発展

1の段から9の段までを二次元リストで返す関数も書いてください。
