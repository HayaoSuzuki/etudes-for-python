---
title: "007: アッカーマンの深淵"
description: "再帰的に定義された関数を読み、m=3の場合を大きなnまで計算する。"
difficulty: 4
---

# 007: アッカーマンの深淵

[ヒント](../hints/007-ackermann-function.md) / [解答](../solutions/007-ackermann-function.md)

**難易度:** ☆☆☆☆

## 問題

**アッカーマン関数** `A(m, n)` は、非負整数 `m` と `n` に対して次のように定義されます。

- `m == 0` のとき、`A(m, n) = n + 1`
- `m > 0` かつ `n == 0` のとき、`A(m, n) = A(m - 1, 1)`
- `m > 0` かつ `n > 0` のとき、`A(m, n) = A(m - 1, A(m, n - 1))`

`m = 3` に固定して、`A(3, n)` を返す関数 `ackermann_3` を書いてください。

## 制約

- `n` は0以上10000以下の整数です。
- `ackermann_3(10000)` を現実的な時間で計算できるようにしてください。

## 例

```python
>>> ackermann_3(0)
5
>>> ackermann_3(1)
13
>>> ackermann_3(2)
29
>>> ackermann_3(10)
8189

```

## 目標

`A(3, 10000)` は大きい整数です。
値そのものを画面にすべて表示する必要はありません。
まず、次の性質を確認してください。

```python
>>> ackermann_3(10000).bit_length()
10003
>>> len(str(ackermann_3(10000)))
3012

```

## 参考

- [アッカーマン関数](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%83%83%E3%82%AB%E3%83%BC%E3%83%9E%E3%83%B3%E9%96%A2%E6%95%B0)
