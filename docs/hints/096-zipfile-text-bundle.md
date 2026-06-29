---
title: "096: 「文字列たちをZIPに束ねる」のヒント"
description: "zipfileで複数のテキストをメモリ上のZIPファイルへまとめる。"
difficulty: 4
---

# 096: 「文字列たちをZIPに束ねる」のヒント

[問題](../problems/096-zipfile-text-bundle.md) / [解答](../solutions/096-zipfile-text-bundle.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    ファイルを作らずにバイト列を読み書きしたい場合は、`io.BytesIO` が使えます。

??? tip "ヒント2"

    `ZipFile` はファイルオブジェクトも受け取れます。
    書き込み時は `"w"`、読み込み時は `"r"` を指定します。

??? tip "ヒント3"

    ZIP内に文字列を書き込むには、`writestr(name, text)` が使えます。
    読み出すときは `read(name)` でバイト列を得て、UTF-8でデコードします。

??? tip "ヒント4"

    ディレクトリ項目は名前が `/` で終わります。
    `namelist()` をソートして処理し、ディレクトリ項目を飛ばします。
