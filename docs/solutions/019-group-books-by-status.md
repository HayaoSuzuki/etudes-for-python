---
title: "019: 「積読たちの仕分け係」の解答"
description: "本の辞書リストを状態ごとにまとめる。"
difficulty: 3
---

# 019: 「積読たちの仕分け係」の解答

[問題](../problems/019-group-books-by-status.md) / [ヒント](../hints/019-group-books-by-status.md)

**難易度:** ☆☆☆

## 方針

本を1冊ずつ見て、状態を取り出します。
その状態が結果の辞書にまだなければ空リストを用意し、そこへタイトルを追加します。

## 実装

```python
def group_titles_by_status(books):
    grouped = {}
    for book in books:
        status = book["status"]
        title = book["title"]
        if status not in grouped:
            grouped[status] = []
        grouped[status].append(title)
    return grouped
```

## 確認

```python
books = [
    {"title": "Python", "status": "reading"},
    {"title": "Math", "status": "waiting"},
    {"title": "SQL", "status": "reading"},
]
assert group_titles_by_status(books) == {"reading": ["Python", "SQL"], "waiting": ["Math"]}
assert group_titles_by_status([]) == {}
```

## 発展

冊数だけを返すなら、リストではなく整数を値にします。
初めて出た状態では1にし、すでにある状態では1を足します。

