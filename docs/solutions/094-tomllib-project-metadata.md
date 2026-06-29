---
title: "094: 「TOMLの中のプロジェクト名」の解答"
description: "tomllib.loadsでTOML文字列を辞書へ変換し、projectテーブルを検査する。"
difficulty: 3
---

# 094: 「TOMLの中のプロジェクト名」の解答

[問題](../problems/094-tomllib-project-metadata.md) / [ヒント](../hints/094-tomllib-project-metadata.md)

**難易度:** ☆☆☆

## 方針

`tomllib.loads` でTOML文字列を辞書に変換します。
`project` テーブルを取り出し、必須キーである `name` と `version` を確認します。

`dependencies` は省略可能なので、省略時は空リストとして扱います。

## 実装

```python
import tomllib


def read_project_metadata(toml_text):
    data = tomllib.loads(toml_text)
    project = data.get("project")
    if not isinstance(project, dict):
        raise ValueError("project table is required")

    if "name" not in project:
        raise ValueError("project.name is required")
    if "version" not in project:
        raise ValueError("project.version is required")

    dependencies = project.get("dependencies", [])
    return {
        "name": project["name"],
        "version": project["version"],
        "dependency_count": len(dependencies),
    }
```

## 確認

```python
text = """
[project]
name = "sample"
version = "1.2.0"
dependencies = ["requests", "rich"]
"""

assert read_project_metadata(text) == {
    "name": "sample",
    "version": "1.2.0",
    "dependency_count": 2,
}

try:
    read_project_metadata("[tool.example]\nname = 'x'\n")
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

`tomllib` は読み込み専用です。
TOMLを書き出したい場合は、標準ライブラリだけでは足りないため、別のライブラリの導入を検討します。

## 参考

- [tomllib](https://docs.python.org/ja/3.14/library/tomllib.html)
