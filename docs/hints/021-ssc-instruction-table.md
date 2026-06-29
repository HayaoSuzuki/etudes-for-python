---
title: "021: 「命令表はコードでもある」のヒント"
description: "8ビット命令をopcodeとoperandに分け、命令表から相互変換する。"
difficulty: 1
---

# 021: 「命令表はコードでもある」のヒント

[問題](../problems/021-ssc-instruction-table.md) / [解答](../solutions/021-ssc-instruction-table.md)

**難易度:** ☆
??? tip "ヒント1"

    上位3ビットを取り出すには、右に5ビットシフトします。

??? tip "ヒント2"

    下位5ビットを取り出すには、`0b11111` とのビットANDを使います。

??? tip "ヒント3"

    命令名からopcodeを引く辞書と、opcodeから命令名を引く辞書を両方作ると実装が単純になります。

