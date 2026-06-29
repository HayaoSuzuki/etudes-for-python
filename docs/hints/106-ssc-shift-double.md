---
title: "106: 「左に寄せれば二倍になる」のヒント"
description: "Shift命令を使って入力値を2倍し、SSCで出力する。"
difficulty: 3
---

# 106: 「左に寄せれば二倍になる」のヒント

[問題](../problems/106-ssc-shift-double.md) / [解答](../solutions/106-ssc-shift-double.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `Read` は入力を直接Accumulatorへ入れる命令ではありません。指定番地へ保存します。

??? tip "ヒント2"

    `Shift` はメモリではなくAccumulatorを変更します。

??? tip "ヒント3"

    出力命令 `Write` は、Accumulatorではなく指定番地の内容を出力します。

