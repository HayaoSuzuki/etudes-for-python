---
title: "064: 「一時作業場でファイルを選ぶ」のヒント"
description: "tempfile.TemporaryDirectoryとshutil.copy2で対象ファイルを一時ディレクトリへコピーする。"
difficulty: 4
---

# 064: 「一時作業場でファイルを選ぶ」のヒント

[問題](../problems/064-tempfile-shutil-workdir.md) / [解答](../solutions/064-tempfile-shutil-workdir.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `TemporaryDirectory` は、一時ディレクトリを作り、`with` ブロックを出ると削除します。

??? tip "ヒント2"

    `Path(source).iterdir()` で、ディレクトリ直下の項目を列挙できます。
    サブディレクトリは対象外なので、`is_file()` を確認します。

??? tip "ヒント3"

    `shutil.copy2(src, dst)` は、ファイル内容とメタデータをコピーします。
    一時ディレクトリ側に同じ名前でコピーします。

??? tip "ヒント4"

    コピー後、一時ディレクトリ内のファイルを名前順に読み、辞書へ入れます。
    `TemporaryDirectory` の外へ出る前に内容を読み終える必要があります。

