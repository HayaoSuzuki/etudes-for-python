---
title: "006: ログから失敗の傾向を読む"
description: "pathlibでログを集め、正規表現とCounterでERRORコード別の要約を作る。"
difficulty: 2
---

# 006: ログから失敗の傾向を読む

[ヒント](../hints/006-pathlib-log-finder.md) / [解答](../solutions/006-pathlib-log-finder.md)

**難易度:** ☆☆
## 問題

関数 `log_error_summary(root)` を書いてください。
この関数は、指定されたディレクトリ以下にある `.log` ファイルを再帰的に探し、`ERROR` 行を集計します。

対象になる `ERROR` 行は、次の形式です。

```text
ERROR CODE message
```

`CODE` は英大文字、数字、アンダースコアからなる文字列です。
戻り値は、次のキーを持つ辞書にしてください。

- `"files"`：`ERROR` 行を1つ以上含んだログファイルの相対パス一覧
- `"codes"`：エラーコードごとの件数を表す辞書
- `"errors"`：`(relative_path, line_number, code, message)` のリスト

ファイルとエラー行は、相対パスの昇順、同じファイル内では行番号の昇順で並べます。
`"codes"` のキーは、コード名の昇順にしてください。

## 制約

- `pathlib.Path` を使ってください。
- `re` を使って `ERROR` 行を解析してください。
- エラーコードの件数集計には `collections.Counter` を使ってください。
- `root` は文字列または `Path` とします。
- ファイルはUTF-8として読んでください。
- 相対パスの区切りは `/` にしてください。
- 形式に合わない行は無視してください。

## 例

```python
>>> from pathlib import Path
>>> from tempfile import TemporaryDirectory
>>> with TemporaryDirectory() as d:
...     root = Path(d)
...     (root / "app.log").write_text("INFO start\nERROR DB down\nERROR API timeout\n", encoding="utf-8")
...     (root / "old.txt").write_text("ERROR DB ignored\n", encoding="utf-8")
...     (root / "sub").mkdir()
...     (root / "sub" / "worker.log").write_text("WARN slow\nERROR DB locked\n", encoding="utf-8")
...     log_error_summary(root)
{'files': ['app.log', 'sub/worker.log'], 'codes': {'API': 1, 'DB': 2}, 'errors': [('app.log', 2, 'DB', 'down'), ('app.log', 3, 'API', 'timeout'), ('sub/worker.log', 2, 'DB', 'locked')]}
```

## 発展

`WARNING` 行も対象にし、レベルごとに件数を分けて返してください。

## 参考

- [pathlib](https://docs.python.org/ja/3.14/library/pathlib.html)
- [re](https://docs.python.org/ja/3.14/library/re.html)
- [collections.Counter](https://docs.python.org/ja/3.14/library/collections.html#collections.Counter)