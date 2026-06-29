---
title: "026: 止まらない二倍の列"
description: "Python整数版のShiftループと8ビット符号付き解釈の停止条件を比較する。"
difficulty: 2
---

# 026: 止まらない二倍の列

[ヒント](../hints/026-ssc-shift-stop-condition.md) / [解答](../solutions/026-ssc-shift-stop-condition.md)

**難易度:** ☆☆
## 問題

Shift命令で値を2倍し続けるプログラムを考えます。
Python整数でデータを扱うSSCでは、正の値を2倍し続けてもオーバーフローしません。
そのため、Accumulatorが正の限り分岐する `Jump` だけでは停止しません。

この違いを確かめるため、次の2つの関数を書いてください。

- `python_shift_outputs(initial, count)`：Python整数として、`initial` を `count` 回だけ2倍した値のリストを返す。
- `signed8_shift_until_stop(initial)`：8ビット符号付き整数として2倍し、値が0以下になったところまでのリストを返す。

8ビット符号付き整数では、0から127を非負、128から255を負の値として解釈します。

## 制約

- SSC本体のデータはPython整数として扱う方針のままです。
- `signed8_shift_until_stop` は、8ビット符号付きとして見たときの停止条件を示すための別関数です。

## 例

```python
>>> python_shift_outputs(3, 6)
[6, 12, 24, 48, 96, 192]
>>> signed8_shift_until_stop(3)
[6, 12, 24, 48, 96, -64]
>>> signed8_shift_until_stop(5)
[10, 20, 40, 80, -96]
```

## 発展

Python整数版のSSCで同じループを実行すると、`max_steps` に達するまで停止しないことを確認してください。

