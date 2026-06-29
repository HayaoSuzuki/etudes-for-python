---
title: "064: 一時作業場でファイルを選ぶ"
description: "tempfile.TemporaryDirectoryとshutil.copy2で対象ファイルを一時ディレクトリへコピーする。"
difficulty: 4
---

# 064: 一時作業場でファイルを選ぶ

[ヒント](../hints/064-tempfile-shutil-workdir.md) / [解答](../solutions/064-tempfile-shutil-workdir.md)

**難易度:** ☆☆☆☆

## 問題

関数 `snapshot_matching_files(source, suffix)` を書いてください。

この関数は、`source` ディレクトリ直下にあるファイルのうち、名前が `suffix` で終わるものを一時作業ディレクトリへコピーし、その内容を辞書で返します。

## 制約

- `tempfile.TemporaryDirectory` を使ってください。
- `shutil.copy2` を使ってください。
- `source` は文字列または `pathlib.Path` です。
- サブディレクトリの中は探索しません。
- ファイルはUTF-8のテキストとして読みます。
- 戻り値は、ファイル名から本文への辞書です。
- ファイル名の昇順で処理してください。

## 例

```python
>>> from pathlib import Path
>>> from tempfile import TemporaryDirectory
>>> with TemporaryDirectory() as d:
...     root = Path(d)
...     (root / "a.txt").write_text("A", encoding="utf-8")
...     (root / "b.md").write_text("B", encoding="utf-8")
...     (root / "c.txt").write_text("C", encoding="utf-8")
...     snapshot_matching_files(root, ".txt")
{'a.txt': 'A', 'c.txt': 'C'}
```

## 発展

サブディレクトリも再帰的に探索し、相対パスをキーにしてください。

## 参考

- [tempfile](https://docs.python.org/ja/3.14/library/tempfile.html)
- [shutil](https://docs.python.org/ja/3.14/library/shutil.html)

