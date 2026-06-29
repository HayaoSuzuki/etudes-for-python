---
title: "058: 「Accumulatorは一つだけ」のヒント"
description: "PC、Accumulator、Memoryを持つSSCを1命令だけ進める。"
difficulty: 4
---

# 058: 「Accumulatorは一つだけ」のヒント

[問題](../problems/058-ssc-step.md) / [解答](../solutions/058-ssc-step.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    現在の命令は `machine["memory"][machine["pc"]]` から読みます。

??? tip "ヒント2"

    各命令は、Accumulator、メモリ、入出力、PCのどれかを変えます。

??? tip "ヒント3"

    通常は `pc + 1` に進み、`Jump` で条件が成り立つ場合だけ別の番地へ進みます。
