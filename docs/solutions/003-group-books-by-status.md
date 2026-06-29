---
title: "003: 「あの日の貸出カード」の解答"
description: "辞書で状態別に集計し、期限切れ候補をソートしてタイトルを取り出す。"
difficulty: 1
---

# 003: 「あの日の貸出カード」の解答

[問題](../problems/003-group-books-by-status.md) / [ヒント](../hints/003-group-books-by-status.md)

**難易度:** ☆
## 方針

1冊ずつ見ながら、状態別のタイトル一覧と冊数を更新します。
同じループの中で期限切れも判定できます。

期限切れ一覧は、タイトルだけを集めると期限順に並べ替えられません。
そこで、期限、入力順、タイトルをタプルにして集め、最後にタイトルだけを取り出します。

## 実装

```python
def reading_report(books, today):
    by_status = {}
    counts = {}
    overdue_candidates = []

    for index, book in enumerate(books):
        title = book["title"]
        status = book["status"]
        due = book["due"]

        if status not in by_status:
            by_status[status] = []
            counts[status] = 0
        by_status[status].append(title)
        counts[status] += 1

        if status != "done" and due < today:
            overdue_candidates.append((due, index, title))

    overdue = [title for due, index, title in sorted(overdue_candidates)]
    return {"by_status": by_status, "counts": counts, "overdue": overdue}
```

## 確認

```python
books = [
    {"title": "Python", "status": "reading", "due": "2026-07-10"},
    {"title": "Math", "status": "waiting", "due": "2026-06-20"},
    {"title": "SQL", "status": "reading", "due": "2026-06-25"},
    {"title": "Done", "status": "done", "due": "2026-06-01"},
]
assert reading_report(books, "2026-06-30") == {
    "by_status": {
        "reading": ["Python", "SQL"],
        "waiting": ["Math"],
        "done": ["Done"],
    },
    "counts": {"reading": 2, "waiting": 1, "done": 1},
    "overdue": ["Math", "SQL"],
}
assert reading_report([], "2026-06-30") == {
    "by_status": {},
    "counts": {},
    "overdue": [],
}
```

## 発展

状態ごとの期限切れ冊数を返す場合は、`overdue_counts` という辞書を追加します。
期限切れと判定したところで、その本の `status` に対応する数を1増やします。