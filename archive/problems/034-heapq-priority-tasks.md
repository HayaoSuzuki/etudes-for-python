---
title: "034: 急ぎの仕事から出てくる"
description: "heapqで優先度付きキューを作り、同じ優先度では投入順を保つ。"
difficulty: 4
---

# 034: 急ぎの仕事から出てくる

[ヒント](../hints/034-heapq-priority-tasks.md) / [解答](../solutions/034-heapq-priority-tasks.md)

**難易度:** ☆☆☆☆

## 問題

クラス `TaskQueue` を書いてください。

`TaskQueue` は、優先度付きのタスクキューです。
数値の小さい優先度ほど先に取り出します。
同じ優先度のタスクは、追加された順に取り出します。

## 制約

- `heapq` を使ってください。
- `push(name, priority)` はタスクを追加し、`None` を返します。
- `pop()` は次のタスク名を返します。
- 空のキューから `pop()` した場合は `IndexError` を送出してください。
- `len(queue)` で残りのタスク数を返してください。
- 同じ優先度のタスクどうしを、タスク名で比較してはいけません。

## 例

```python
>>> queue = TaskQueue()
>>> queue.push("write report", 2)
>>> queue.push("fix bug", 1)
>>> queue.push("review", 1)
>>> [queue.pop(), queue.pop(), queue.pop()]
['fix bug', 'review', 'write report']
>>> len(queue)
0
>>> queue.pop()
Traceback (most recent call last):
...
IndexError: pop from empty task queue
```

## 発展

タスクを削除済みとして印を付け、まだ取り出されていないタスクをキャンセルできるようにしてください。

## 参考

- [heapq](https://docs.python.org/ja/3.14/library/heapq.html)

