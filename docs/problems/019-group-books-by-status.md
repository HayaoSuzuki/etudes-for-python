---
title: "019: 積読たちの仕分け係"
description: "本の辞書リストを状態ごとにまとめる。"
difficulty: 3
---

# 019: 積読たちの仕分け係

[ヒント](../hints/019-group-books-by-status.md) / [解答](../solutions/019-group-books-by-status.md)

**難易度:** ☆☆☆

## 問題

関数 `group_titles_by_status(books)` を書いてください。
この関数は、本を表す辞書のリスト `books` を受け取り、状態ごとにタイトルをまとめた辞書を返します。

各本の辞書には、`"title"` と `"status"` のキーがあります。
返す辞書では、状態をキー、タイトルのリストを値にしてください。
タイトルの順番は、入力に出てきた順番を保ちます。

## 制約

- `books` は辞書のリストです。
- 各辞書には `"title"` と `"status"` があります。
- 状態の種類は決まっていません。

## 例

```python
>>> books = [
...     {"title": "Python", "status": "reading"},
...     {"title": "Math", "status": "waiting"},
...     {"title": "SQL", "status": "reading"},
... ]
>>> group_titles_by_status(books)
{'reading': ['Python', 'SQL'], 'waiting': ['Math']}
>>> group_titles_by_status([])
{}
```

## 発展

状態ごとの冊数だけを返す関数も書いてください。

