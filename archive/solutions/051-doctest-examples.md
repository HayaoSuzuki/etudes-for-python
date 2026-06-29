---
title: "051: 「例はそのまま試験になる」の解答"
description: "DocTestParserとDocTestRunnerで文字列中のdoctest例を検査する。"
difficulty: 3
---

# 051: 「例はそのまま試験になる」の解答

[問題](../problems/051-doctest-examples.md) / [ヒント](../hints/051-doctest-examples.md)

**難易度:** ☆☆☆

## 方針

`DocTestParser` で文字列からテストを作り、`DocTestRunner` で実行します。
`runner.run` の戻り値には `attempted` と `failed` が入っているので、それを辞書に詰め替えます。

失敗内容を表示しないため、`out` に何もしない関数を渡します。

## 実装

```python
import doctest


def run_doc_examples(source, namespace=None):
    if namespace is None:
        namespace = {}

    parser = doctest.DocTestParser()
    test = parser.get_doctest(source, namespace.copy(), "snippet", None, 0)

    runner = doctest.DocTestRunner(verbose=False)
    result = runner.run(test, out=lambda text: None)

    return {
        "attempted": result.attempted,
        "failed": result.failed,
    }
```

## 確認

```python
source = """>>> 1 + 1
2
>>> len("abc")
3
"""

assert run_doc_examples(source) == {"attempted": 2, "failed": 0}
assert run_doc_examples(">>> 1 + 1\n3\n") == {"attempted": 1, "failed": 1}
assert run_doc_examples(">>> double(4)\n8\n", {"double": lambda n: n * 2}) == {
    "attempted": 1,
    "failed": 0,
}
```

## 発展

`DocTestRunner` には `optionflags` を渡せます。
`doctest.ELLIPSIS` や `doctest.NORMALIZE_WHITESPACE` を指定できるようにすると、出力の一部だけを検査する例にも対応できます。

## 参考

- [doctest](https://docs.python.org/ja/3.14/library/doctest.html)

