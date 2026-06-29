---
title: "083: 「同じ形の試験を並べる」の解答"
description: "slug化関数を実装し、unittestのsubTestで複数ケースを検査する。"
difficulty: 3
---

# 083: 「同じ形の試験を並べる」の解答

[問題](../problems/083-unittest-table-cases.md) / [ヒント](../hints/083-unittest-table-cases.md)

**難易度:** ☆☆☆

## 方針

`make_slug` は、入力文字列を1文字ずつ走査します。
ASCII英数字は小文字にして残し、それ以外の連続は1つのハイフンにまとめます。

テストでは、入力と期待値の組を並べ、`subTest` の中で同じ検査を繰り返します。

## 実装

```python
import unittest


def make_slug(text):
    parts = []
    last_was_separator = False

    for ch in text.lower():
        if ch.isascii() and ch.isalnum():
            parts.append(ch)
            last_was_separator = False
        elif not last_was_separator:
            parts.append("-")
            last_was_separator = True

    return "".join(parts).strip("-")


class MakeSlugTests(unittest.TestCase):
    def test_make_slug(self):
        cases = [
            ("Hello, Python 3!", "hello-python-3"),
            ("  Already--Slug  ", "already-slug"),
            ("日本語", ""),
            ("A__B__C", "a-b-c"),
        ]

        for text, expected in cases:
            with self.subTest(text=text):
                self.assertEqual(make_slug(text), expected)
```

## 確認

```python
from io import StringIO


assert make_slug("Hello, Python 3!") == "hello-python-3"
assert make_slug("  Already--Slug  ") == "already-slug"
assert make_slug("日本語") == ""

suite = unittest.defaultTestLoader.loadTestsFromTestCase(MakeSlugTests)
result = unittest.TextTestRunner(stream=StringIO(), verbosity=0).run(suite)
assert result.wasSuccessful()
```

## 発展

テストケースが増える場合は、ケースのリストをテストクラスの外に出すと、実装と期待値を別々に読めます。
ただし、テストデータが複雑になりすぎると、失敗時の原因が追いにくくなります。

## 参考

- [unittest](https://docs.python.org/ja/3.14/library/unittest.html)
