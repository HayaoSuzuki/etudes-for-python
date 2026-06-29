---
title: "063: 「文字列たちをZIPに束ねる」の解答"
description: "BytesIOとZipFileでメモリ上のZIPファイルを読み書きする。"
difficulty: 4
---

# 063: 「文字列たちをZIPに束ねる」の解答

[問題](../problems/063-zipfile-text-bundle.md) / [ヒント](../hints/063-zipfile-text-bundle.md)

**難易度:** ☆☆☆☆

## 方針

`BytesIO` を使うと、ファイルのように扱えるメモリ上のバイト列を作れます。
これを `ZipFile` に渡して、実ファイルを作らずにZIPを読み書きします。

書き込みでは `writestr`、読み込みでは `read` を使います。

## 実装

```python
from io import BytesIO
from zipfile import ZIP_DEFLATED, ZipFile


def make_text_zip(files):
    buffer = BytesIO()
    with ZipFile(buffer, "w", compression=ZIP_DEFLATED) as archive:
        for name in sorted(files):
            archive.writestr(name, files[name])
    return buffer.getvalue()


def read_text_zip(data):
    result = {}
    with ZipFile(BytesIO(data), "r") as archive:
        for name in sorted(archive.namelist()):
            if name.endswith("/"):
                continue
            result[name] = archive.read(name).decode("utf-8")
    return result
```

## 確認

```python
data = make_text_zip({"b.txt": "B", "a.txt": "A"})
assert read_text_zip(data) == {"a.txt": "A", "b.txt": "B"}
```

## 発展

ZIPファイルには同じ名前の項目を複数入れることもできます。
辞書へ戻す設計では同名項目を表現できないため、重複をどう扱うか仕様として決める必要があります。

## 参考

- [zipfile](https://docs.python.org/ja/3.14/library/zipfile.html)

