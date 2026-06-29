---
title: "025: 「Jump 0で眠る機械」のヒント"
description: "SSCプログラムを停止命令まで実行し、出力を返す。"
difficulty: 2
---

# 025: 「Jump 0で眠る機械」のヒント

[問題](../problems/025-ssc-run.md) / [解答](../solutions/025-ssc-run.md)

**難易度:** ☆☆
??? tip "ヒント1"

    まず `make_machine(program, inputs)` で初期状態を作ります。

??? tip "ヒント2"

    `machine["halted"]` が真になるまで `step()` を繰り返します。

??? tip "ヒント3"

    無限ループするプログラムに備えて、実行した命令数を数えます。

