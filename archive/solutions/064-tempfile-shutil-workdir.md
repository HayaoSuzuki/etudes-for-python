---
title: "064: 「一時作業場でファイルを選ぶ」の解答"
description: "TemporaryDirectoryに対象ファイルをcopy2し、コピー先から内容を読み取る。"
difficulty: 4
---

# 064: 「一時作業場でファイルを選ぶ」の解答

[問題](../problems/064-tempfile-shutil-workdir.md) / [ヒント](../hints/064-tempfile-shutil-workdir.md)

**難易度:** ☆☆☆☆

## 方針

一時作業ディレクトリを作り、対象ファイルだけをそこへコピーします。
コピー先から内容を読み取って辞書を作り、`with` ブロックを出る前に返します。

`TemporaryDirectory` の管理下にあるディレクトリは、処理後に削除されます。

## 実装

```python
from pathlib import Path
from shutil import copy2
from tempfile import TemporaryDirectory


def snapshot_matching_files(source, suffix):
    source = Path(source)

    with TemporaryDirectory() as directory:
        workspace = Path(directory)

        for path in sorted(source.iterdir(), key=lambda item: item.name):
            if path.is_file() and path.name.endswith(suffix):
                copy2(path, workspace / path.name)

        return {
            path.name: path.read_text(encoding="utf-8")
            for path in sorted(workspace.iterdir(), key=lambda item: item.name)
        }
```

## 確認

```python
from pathlib import Path
from tempfile import TemporaryDirectory


with TemporaryDirectory() as d:
    root = Path(d)
    (root / "a.txt").write_text("A", encoding="utf-8")
    (root / "b.md").write_text("B", encoding="utf-8")
    (root / "c.txt").write_text("C", encoding="utf-8")

    assert snapshot_matching_files(root, ".txt") == {
        "a.txt": "A",
        "c.txt": "C",
    }
```

## 発展

一時ディレクトリを使うと、途中で作る作業ファイルを処理後に残さずに済みます。
ただし、戻り値として一時ディレクトリ内のパスを返すと、呼び出し側が使う時点では消えている可能性があります。

## 参考

- [tempfile](https://docs.python.org/ja/3.14/library/tempfile.html)
- [shutil](https://docs.python.org/ja/3.14/library/shutil.html)

