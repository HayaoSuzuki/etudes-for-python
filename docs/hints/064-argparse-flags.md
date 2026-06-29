---
title: "064: 「旗を立てれば設定が歩く」のヒント"
description: "argparseでコマンドライン引数を解析し、設定辞書に変換する。"
difficulty: 3
---

# 064: 「旗を立てれば設定が歩く」のヒント

[問題](../problems/064-argparse-flags.md) / [解答](../solutions/064-argparse-flags.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `ArgumentParser` に位置引数とオプションを登録してから、`parse_args(args)` を呼びます。

??? tip "ヒント2"

    `--width` と `--height` は `type=int` を指定すると整数に変換されます。
    必須オプションにするには `required=True` を使います。

??? tip "ヒント3"

    `--format` は `choices=["png", "jpg"]` と `default="png"` を指定できます。
    `--keep-aspect` は `action="store_true"` が使えます。

??? tip "ヒント4"

    `parse_args` の戻り値は `Namespace` です。
    `vars(namespace)` で辞書に変換できます。
