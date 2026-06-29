---
title: "066: 「外のコマンドの返事を読む」のヒント"
description: "subprocess.runで外部コマンドを実行し、終了コードと出力を整理する。"
difficulty: 4
---

# 066: 「外のコマンドの返事を読む」のヒント

[問題](../problems/066-subprocess-result-parser.md) / [解答](../solutions/066-subprocess-result-parser.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `subprocess.run(args)` は外部コマンドを実行し、結果を `CompletedProcess` として返します。

??? tip "ヒント2"

    標準出力と標準エラーを捕捉するには、`capture_output=True` を指定します。
    文字列として受け取りたい場合は `text=True` を指定します。

??? tip "ヒント3"

    終了コードが0でなくても例外にしないため、`check=False` にします。

??? tip "ヒント4"

    `stdout` と `stderr` は `splitlines()` で行ごとのリストにできます。
    `ok` は `returncode == 0` で判定します。

