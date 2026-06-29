---
title: "007: 驚くべき関数"
description: "負の整数を含めて、整数が奇数かどうかを判定する関数を書く。"
difficulty: 1
---

# 007: 驚くべき関数

[ヒント](../hints/007-even-or-odd.md) / [解答](../solutions/007-even-or-odd.md)

**難易度:** ☆

## 問題

整数 `n` を受け取り、`n` が奇数なら `True`、偶数なら `False` を返す関数 `is_odd` を書いてください。

`n` が負の場合も正しく扱ってください。

## 制約

- `n` は整数です。
- 正の整数、0、負の整数のいずれも扱います。

## 例

```python
>>> is_odd(3)
True
>>> is_odd(4)
False
>>> is_odd(0)
False
>>> is_odd(-3)
True
```

## 発展

`is_even` も同じ方針で書いてください。
