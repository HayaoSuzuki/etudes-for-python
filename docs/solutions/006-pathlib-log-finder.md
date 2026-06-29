---
title: "006: 「ログから失敗の傾向を読む」の解答"
description: "Path.rglob、正規表現、Counterを組み合わせてログの要約を作る。"
difficulty: 2
---

# 006: 「ログから失敗の傾向を読む」の解答

[問題](../problems/006-pathlib-log-finder.md) / [ヒント](../hints/006-pathlib-log-finder.md)

**難易度:** ☆☆
## 方針

ログファイルは `Path.rglob` で集めます。
相対パスでソートしてから読むと、戻り値の順番が実行環境に左右されません。

各行は正規表現で解析します。
一致した行だけを詳細リストに追加し、同時に `Counter` でコード別の件数を更新します。

## 実装

```python
from collections import Counter
from pathlib import Path
import re


ERROR_PATTERN = re.compile(r"^ERROR\s+([A-Z0-9_]+)\s+(.*)$")


def log_error_summary(root):
    root = Path(root)
    files = []
    codes = Counter()
    errors = []

    paths = sorted(root.rglob("*.log"), key=lambda path: path.relative_to(root).as_posix())
    for path in paths:
        relative_path = path.relative_to(root).as_posix()
        has_error = False
        lines = path.read_text(encoding="utf-8").splitlines()
        for line_number, line in enumerate(lines, start=1):
            match = ERROR_PATTERN.match(line)
            if match is None:
                continue
            code, message = match.groups()
            has_error = True
            codes[code] += 1
            errors.append((relative_path, line_number, code, message))
        if has_error:
            files.append(relative_path)

    return {
        "files": files,
        "codes": dict(sorted(codes.items())),
        "errors": errors,
    }
```

## 確認

```python
from pathlib import Path
from tempfile import TemporaryDirectory


with TemporaryDirectory() as d:
    root = Path(d)
    (root / "app.log").write_text(
        "INFO start\nERROR DB down\nERROR API timeout\n",
        encoding="utf-8",
    )
    (root / "old.txt").write_text("ERROR DB ignored\n", encoding="utf-8")
    (root / "sub").mkdir()
    (root / "sub" / "worker.log").write_text(
        "WARN slow\nERROR DB locked\n",
        encoding="utf-8",
    )

    assert log_error_summary(root) == {
        "files": ["app.log", "sub/worker.log"],
        "codes": {"API": 1, "DB": 2},
        "errors": [
            ("app.log", 2, "DB", "down"),
            ("app.log", 3, "API", "timeout"),
            ("sub/worker.log", 2, "DB", "locked"),
        ],
    }
```

## 発展

`WARNING` 行も扱う場合は、正規表現の先頭を `(ERROR|WARNING)` に変えます。
戻り値では、レベルとコードの組み合わせをキーにするか、レベルごとに別の `Counter` を持つと整理しやすくなります。

## 参考

- [pathlib](https://docs.python.org/ja/3.14/library/pathlib.html)
- [re](https://docs.python.org/ja/3.14/library/re.html)
- [collections.Counter](https://docs.python.org/ja/3.14/library/collections.html#collections.Counter)