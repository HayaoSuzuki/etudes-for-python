---
title: "002: Hello world 2nd stageのヒント"
description: "sys.stdinとsys.stdoutを使って入出力を行う。"
---

# 002: Hello world 2nd stageのヒント

[問題](../problems/002-hello-world-2nd-stage.md) / [解答](../solutions/002-hello-world-2nd-stage.md)

??? tip "ヒント1"

    Pythonでは、`sys` モジュールから標準入力と標準出力を扱えます。

??? tip "ヒント2"

    `sys.stdin.readline()` は標準入力から1行を読みます。
    読み取った文字列には、行末の改行が含まれます。

??? tip "ヒント3"

    `sys.stdout.write()` は文字列を標準出力へ書きます。
    `print()` と違い、改行は自動では付きません。
