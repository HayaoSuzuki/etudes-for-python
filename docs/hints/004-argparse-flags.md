---
title: "004: 「売上レポートの入口を作る」のヒント"
description: "argparseで選択肢、真偽フラグ、独自の型変換を扱う。"
difficulty: 1
---

# 004: 「売上レポートの入口を作る」のヒント

[問題](../problems/004-argparse-flags.md) / [解答](../solutions/004-argparse-flags.md)

**難易度:** ☆
??? tip "ヒント1"

    `choices` を使うと、`--format` の値を `table` と `json` に制限できます。
    真偽フラグは `action="store_true"` で扱えます。

??? tip "ヒント2"

    `--tax-rate` のように変換と検査を同時にしたい値は、独自の関数を `type` に渡せます。
    検査に失敗したら `argparse.ArgumentTypeError` を送出します。

??? tip "ヒント3"

    `YYYY-MM` の検査では、長さ、5文字目のハイフン、年と月が数字かどうかを見ます。
    月が `01` から `12` の範囲にあることも確認します。

??? tip "ヒント4"

    `parse_args` の戻り値は `Namespace` です。
    `vars(namespace)` を使うと、属性を辞書として取り出せます。