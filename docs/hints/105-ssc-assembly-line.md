---
title: "105: 「ニーモニックの皮をかぶった数」のヒント"
description: "SSCの1行アセンブリを8ビット命令へ変換する。"
difficulty: 3
---

# 105: 「ニーモニックの皮をかぶった数」のヒント

[問題](../problems/105-ssc-assembly-line.md) / [解答](../solutions/105-ssc-assembly-line.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    まず、`;` より前だけを取り出してから `strip()` します。

??? tip "ヒント2"

    `Stop` は特別扱いして、`Jump 0` と同じ命令にします。

??? tip "ヒント3"

    それ以外は、命令名とoperandを `split()` で分けて、operandを整数に変換します。

