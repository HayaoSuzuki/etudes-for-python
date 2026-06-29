---
title: "077: 「エラー行は道の先にある」のヒント"
description: "pathlibでログファイルを再帰的に探し、ERROR行を集める。"
difficulty: 3
---

# 077: 「エラー行は道の先にある」のヒント

[問題](../problems/077-pathlib-log-finder.md) / [解答](../solutions/077-pathlib-log-finder.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `Path(root)` とすると、文字列でも `Path` でも同じように扱えます。

??? tip "ヒント2"

    `Path.rglob("*.log")` は、指定したディレクトリ以下から `.log` ファイルを再帰的に探します。
    順序を安定させるには `sorted()` を使います。

??? tip "ヒント3"

    `read_text(encoding="utf-8")` でファイル全体を文字列として読めます。
    行番号が必要なら、`splitlines()` と `enumerate(..., start=1)` を組み合わせます。

??? tip "ヒント4"

    相対パスは `path.relative_to(root)` で作れます。
    Windowsでも `/` 区切りにしたい場合は、`Path.as_posix()` を使います。
