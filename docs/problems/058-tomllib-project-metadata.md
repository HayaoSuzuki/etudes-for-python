---
title: "058: TOMLの中のプロジェクト名"
description: "tomllibでpyproject.toml形式の文字列を読み、プロジェクト情報を取り出す。"
difficulty: 3
---

# 058: TOMLの中のプロジェクト名

[ヒント](../hints/058-tomllib-project-metadata.md) / [解答](../solutions/058-tomllib-project-metadata.md)

**難易度:** ☆☆☆

## 問題

関数 `read_project_metadata(toml_text)` を書いてください。

この関数は、`pyproject.toml` 形式の文字列から、プロジェクト名、バージョン、依存パッケージ数を取り出します。

## 制約

- `tomllib` を使ってください。
- `toml_text` は文字列です。
- `[project]` テーブルがない場合は `ValueError` を送出してください。
- `name` と `version` がない場合は `ValueError` を送出してください。
- `dependencies` がない場合は空リストとして扱ってください。
- 戻り値は、キー `name`、`version`、`dependency_count` を持つ辞書です。

## 例

```python
>>> text = '''
... [project]
... name = "sample"
... version = "1.2.0"
... dependencies = ["requests", "rich"]
... '''
>>> read_project_metadata(text)
{'name': 'sample', 'version': '1.2.0', 'dependency_count': 2}
```

## 発展

任意依存関係の `[project.optional-dependencies]` も数えてください。

## 参考

- [tomllib](https://docs.python.org/ja/3.14/library/tomllib.html)

