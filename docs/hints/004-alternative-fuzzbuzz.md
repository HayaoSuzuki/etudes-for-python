---
title: "004: Alternative FuzzBuzzのヒント"
description: "倍数条件の包含関係と優先順位を考える。"
---

# 004: Alternative FuzzBuzzのヒント

[問題](../problems/004-alternative-fuzzbuzz.md) / [解答](../solutions/004-alternative-fuzzbuzz.md)

## ヒント1

`range(1, n + 1)` を使うと、1から `n` までの整数を順に取り出せます。

## ヒント2

`i % 6 == 0` なら、`i % 3 == 0` も成り立ちます。
同じことが9の倍数にも成り立ちます。

## ヒント3

この問題では、条件に当たる文字列をすべて足すわけではありません。
6なら `FizzFuzz` ではなく `Fuzz` を返します。

## ヒント4

複数の条件を満たす数では、先に調べた条件が選ばれます。
9、6、3の順に調べると、18は9の倍数として扱えます。
