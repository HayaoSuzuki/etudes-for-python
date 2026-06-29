---
title: "077: エラー行は道の先にある"
description: "pathlibでログファイルを再帰的に探し、ERROR行を集める。"
difficulty: 3
---

# 077: エラー行は道の先にある

[ヒント](../hints/077-pathlib-log-finder.md) / [解答](../solutions/077-pathlib-log-finder.md)

**難易度:** ☆☆☆

## 問題

関数 `find_error_lines(root)` を書いてください。

この関数は、指定されたディレクトリ以下にある `.log` ファイルを再帰的に探し、`ERROR` を含む行を集めます。

戻り値は、`(相対パス, 行番号, 行の内容)` のタプルのリストです。

## 制約

- `pathlib.Path` を使ってください。
- `root` は文字列または `Path` とします。
- `.log` ファイルだけを対象にしてください。
- ファイルはUTF-8として読んでください。
- 行番号は1から始めてください。
- 行末の改行文字は戻り値に含めないでください。
- 探索結果は、相対パスの昇順にしてください。
- 相対パスの区切りは `/` にしてください。

## 例

```python
>>> from pathlib import Path
>>> from tempfile import TemporaryDirectory
>>> with TemporaryDirectory() as d:
...     root = Path(d)
...     (root / "app.log").write_text("INFO start\nERROR bad\n", encoding="utf-8")
...     (root / "old.txt").write_text("ERROR ignored\n", encoding="utf-8")
...     (root / "sub").mkdir()
...     (root / "sub" / "worker.log").write_text("ERROR late\n", encoding="utf-8")
...     find_error_lines(root)
[('app.log', 2, 'ERROR bad'), ('sub/worker.log', 1, 'ERROR late')]
```

## 発展

検索する文字列を引数で指定できるようにしてください。

## 参考

- [pathlib](https://docs.python.org/ja/3.14/library/pathlib.html)
