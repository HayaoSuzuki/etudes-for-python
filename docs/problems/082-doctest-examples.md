---
title: "082: 例はそのまま試験になる"
description: "doctestで対話形式の実行例を検査し、試行数と失敗数を返す。"
difficulty: 3
---

# 082: 例はそのまま試験になる

[ヒント](../hints/082-doctest-examples.md) / [解答](../solutions/082-doctest-examples.md)

**難易度:** ☆☆☆

## 問題

関数 `run_doc_examples(source, namespace=None)` を書いてください。

この関数は、`>>>` で始まる対話形式の実行例を含む文字列を受け取り、`doctest` で検査します。
戻り値は、試行した例の数と失敗した例の数を持つ辞書です。

## 制約

- `doctest` モジュールを使ってください。
- `source` は文字列です。
- `namespace` は、実行例で使う名前を入れた辞書、または `None` です。
- `namespace` が `None` の場合は、空の名前空間として扱ってください。
- 戻り値は、キー `attempted` と `failed` を持つ辞書にしてください。
- 失敗した例があっても、例外を送出せずに失敗数として返してください。
- 失敗内容を標準出力へ表示しないでください。

## 例

```python
>>> source = """>>> 1 + 1
... 2
... >>> len("abc")
... 3
... """
>>> run_doc_examples(source)
{'attempted': 2, 'failed': 0}
>>> run_doc_examples(">>> 1 + 1\n3\n")
{'attempted': 1, 'failed': 1}
>>> run_doc_examples(">>> double(4)\n8\n", {"double": lambda n: n * 2})
{'attempted': 1, 'failed': 0}
```

## 発展

空白の違いを許すなど、`doctest` のオプションを引数で指定できるようにしてください。

## 参考

- [doctest](https://docs.python.org/ja/3.14/library/doctest.html)
