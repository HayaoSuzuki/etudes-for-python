---
title: "058: 「TOMLの中のプロジェクト名」のヒント"
description: "tomllibでpyproject.toml形式の文字列を読み、プロジェクト情報を取り出す。"
difficulty: 3
---

# 058: 「TOMLの中のプロジェクト名」のヒント

[問題](../problems/058-tomllib-project-metadata.md) / [解答](../solutions/058-tomllib-project-metadata.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `tomllib.loads` は、TOML形式の文字列を辞書へ変換します。
    `[project]` は、戻り値の `"project"` キーに対応します。

??? tip "ヒント2"

    必須のテーブルやキーがない場合は、後続処理で `KeyError` に任せるより、明示的に `ValueError` にすると仕様がわかりやすくなります。

??? tip "ヒント3"

    `dependencies` は省略できるので、`project.get("dependencies", [])` のように既定値を補えます。

??? tip "ヒント4"

    戻り値では、依存パッケージの中身ではなく個数だけを返します。
    `len(dependencies)` を `dependency_count` に入れます。

