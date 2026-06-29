---
title: "003: 読書ログは期限を覚えている"
description: "本の一覧から状態別のタイトル、冊数、期限切れの本をまとめたレポートを作る。"
difficulty: 1
---

# 003: 読書ログは期限を覚えている

[ヒント](../hints/003-group-books-by-status.md) / [解答](../solutions/003-group-books-by-status.md)

**難易度:** ☆
## 問題

関数 `reading_report(books, today)` を書いてください。
この関数は、本を表す辞書のリスト `books` と今日の日付 `today` を受け取り、読書ログのレポートを返します。

各本の辞書には、`"title"`、`"status"`、`"due"` のキーがあります。
`"due"` は `"YYYY-MM-DD"` 形式の返却期限です。
`today` も同じ形式の文字列です。

戻り値の辞書は、次のキーを持ちます。

- `"by_status"`：状態ごとのタイトル一覧
- `"counts"`：状態ごとの冊数
- `"overdue"`：期限切れのタイトル一覧

状態ごとのタイトル一覧では、入力に出てきた順番を保ちます。
期限切れの本は、`status` が `"done"` ではなく、`due` が `today` より前の本です。
`"overdue"` は期限の古い順に並べ、同じ期限なら入力順を保ってください。

## 制約

- `books` は辞書のリストです。
- 日付文字列はすべて `YYYY-MM-DD` 形式です。
- 日付の形式チェックはしません。
- 状態の種類は決まっていません。

## 例

```python
>>> books = [
...     {"title": "Python", "status": "reading", "due": "2026-07-10"},
...     {"title": "Math", "status": "waiting", "due": "2026-06-20"},
...     {"title": "SQL", "status": "reading", "due": "2026-06-25"},
...     {"title": "Done", "status": "done", "due": "2026-06-01"},
... ]
>>> reading_report(books, "2026-06-30")
{'by_status': {'reading': ['Python', 'SQL'], 'waiting': ['Math'], 'done': ['Done']}, 'counts': {'reading': 2, 'waiting': 1, 'done': 1}, 'overdue': ['Math', 'SQL']}
>>> reading_report([], "2026-06-30")
{'by_status': {}, 'counts': {}, 'overdue': []}
```

## 発展

状態ごとの期限切れ冊数も返すようにしてください。