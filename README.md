# Etudes for Python

Pythonまたはプログラミング一般の演習書を作るためのMkDocsプロジェクトです。

## セットアップ

```powershell
uv sync --dev
```

## プレビュー

```powershell
uv run mkdocs serve
```

## ビルド

```powershell
uv run mkdocs build --strict
```

## 執筆

1つの演習は、問題、ヒント、解答の3ファイルで管理します。
新しい演習を書くときは、`templates/` 配下のMarkdownファイルを複製して、同じ `NNN-slug` を使ってください。
