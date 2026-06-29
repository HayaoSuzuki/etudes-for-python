---
title: "005: 「九つの積の物語」の解答"
description: "range()とリストを使って、九九の一行を作る。"
difficulty: 1
---

# 005: 「九つの積の物語」の解答

[問題](../problems/005-multiplication-row.md) / [ヒント](../hints/005-multiplication-row.md)

**難易度:** ☆

## 方針

1から9までの数を順に使って、`n` との積をリストに追加します。
`range(1, 10)` は10を含まないので、ちょうど1から9までを表せます。

## 実装

```python
def multiplication_row(n):
    row = []
    for i in range(1, 10):
        row.append(n * i)
    return row
```

## 確認

```python
assert multiplication_row(3) == [3, 6, 9, 12, 15, 18, 21, 24, 27]
assert multiplication_row(9)[-1] == 81
assert multiplication_row(1) == [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## 発展

二次元リストにする場合は、1から9までの `n` について `multiplication_row(n)` を呼び出します。

