---
title: "060: 「エラー行は道の先にある」の解答"
description: "Path.rglobでログを探し、相対パスと行番号を添えてERROR行を返す。"
difficulty: 3
---

# 060: 「エラー行は道の先にある」の解答

[問題](../problems/060-pathlib-log-finder.md) / [ヒント](../hints/060-pathlib-log-finder.md)

**難易度:** ☆☆☆

## 方針

`root` を `Path` に変換してから、`rglob("*.log")` で対象ファイルを探します。
順序を安定させるため、相対パスの文字列でソートします。

各ファイルをUTF-8で読み、`ERROR` を含む行だけを結果に追加します。

## 実装

```python
from pathlib import Path


def find_error_lines(root):
    root = Path(root)
    results = []

    paths = sorted(root.rglob("*.log"), key=lambda path: path.relative_to(root).as_posix())
    for path in paths:
        relative_path = path.relative_to(root).as_posix()
        lines = path.read_text(encoding="utf-8").splitlines()
        for line_number, line in enumerate(lines, start=1):
            if "ERROR" in line:
                results.append((relative_path, line_number, line))

    return results
```

## 確認

```python
from pathlib import Path
from tempfile import TemporaryDirectory


with TemporaryDirectory() as d:
    root = Path(d)
    (root / "app.log").write_text("INFO start\nERROR bad\n", encoding="utf-8")
    (root / "old.txt").write_text("ERROR ignored\n", encoding="utf-8")
    (root / "sub").mkdir()
    (root / "sub" / "worker.log").write_text("ERROR late\n", encoding="utf-8")

    assert find_error_lines(root) == [
        ("app.log", 2, "ERROR bad"),
        ("sub/worker.log", 1, "ERROR late"),
    ]
```

## 発展

実際のログ処理では、ファイルが読めない場合や文字コードが違う場合もあります。
そのような失敗を呼び出し側へ送出するか、警告として記録して処理を続けるかを仕様として決めます。

## 参考

- [pathlib](https://docs.python.org/ja/3.14/library/pathlib.html)

