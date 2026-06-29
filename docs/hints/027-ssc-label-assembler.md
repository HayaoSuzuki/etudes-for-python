---
title: "027: 「ラベルは番地を忘れさせる」のヒント"
description: "ラベルとData擬似命令を持つ小さなSSCアセンブラを書く。"
difficulty: 3
---

# 027: 「ラベルは番地を忘れさせる」のヒント

[問題](../problems/027-ssc-label-assembler.md) / [解答](../solutions/027-ssc-label-assembler.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    1回目の走査では、命令やDataを生成せず、ラベル名と番地だけを記録します。

??? tip "ヒント2"

    ラベルの有無にかかわらず、命令またはDataがある行だけ番地を1つ進めます。

??? tip "ヒント3"

    2回目の走査で、operandが整数に変換できない場合はラベル辞書から番地を引きます。

