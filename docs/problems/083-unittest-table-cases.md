---
title: "083: 同じ形の試験を並べる"
description: "unittestとsubTestで複数の入力例をまとめて検査する。"
difficulty: 3
---

# 083: 同じ形の試験を並べる

[ヒント](../hints/083-unittest-table-cases.md) / [解答](../solutions/083-unittest-table-cases.md)

**難易度:** ☆☆☆

## 問題

関数 `make_slug(text)` と、これを検査する `unittest.TestCase` のサブクラス `MakeSlugTests` を書いてください。

`make_slug(text)` は、見出し文字列からURLなどに使いやすい短い識別子を作ります。

## 制約

- `make_slug(text)` は文字列を受け取り、文字列を返します。
- ASCIIの英数字だけを使ってください。
- 英字は小文字にしてください。
- 英数字以外の連続は、1つのハイフン `-` に置き換えてください。
- 先頭と末尾のハイフンは取り除いてください。
- `MakeSlugTests` は `unittest.TestCase` を継承してください。
- `MakeSlugTests` のテストでは、`subTest` を使って複数のケースを検査してください。

## 例

```python
>>> make_slug("Hello, Python 3!")
'hello-python-3'
>>> make_slug("  Already--Slug  ")
'already-slug'
>>> make_slug("日本語")
''
```

## 発展

Unicode文字も読みやすい形で残す仕様に変えてください。

## 参考

- [unittest](https://docs.python.org/ja/3.14/library/unittest.html)
