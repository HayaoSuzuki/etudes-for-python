---
title: "080: 「急ぎの仕事から出てくる」の解答"
description: "heapqに優先度、投入順、タスク名のタプルを入れて安定した優先度付きキューを作る。"
difficulty: 4
---

# 080: 「急ぎの仕事から出てくる」の解答

[問題](../problems/080-heapq-priority-tasks.md) / [ヒント](../hints/080-heapq-priority-tasks.md)

**難易度:** ☆☆☆☆

## 方針

`heapq` は最小値から取り出すヒープです。
優先度が小さいほど先に出したいので、優先度をそのまま先頭に置けます。

同じ優先度の順序を保つため、追加するたびに増える連番を2番目の要素にします。
これで、タスク名どうしを比較せずに順序が決まります。

## 実装

```python
from heapq import heappop, heappush


class TaskQueue:
    def __init__(self):
        self._heap = []
        self._order = 0

    def push(self, name, priority):
        heappush(self._heap, (priority, self._order, name))
        self._order += 1

    def pop(self):
        if not self._heap:
            raise IndexError("pop from empty task queue")
        _, _, name = heappop(self._heap)
        return name

    def __len__(self):
        return len(self._heap)
```

## 確認

```python
queue = TaskQueue()
queue.push("write report", 2)
queue.push("fix bug", 1)
queue.push("review", 1)

assert [queue.pop(), queue.pop(), queue.pop()] == [
    "fix bug",
    "review",
    "write report",
]
assert len(queue) == 0

try:
    queue.pop()
except IndexError as error:
    assert str(error) == "pop from empty task queue"
else:
    raise AssertionError("IndexError was not raised")
```

## 発展

優先度をあとから変更したい場合、ヒープ内の既存要素を直接探して更新するのは扱いにくくなります。
新しい要素を追加し、古い要素を無効として印を付ける方式にすると実装しやすくなります。

## 参考

- [heapq](https://docs.python.org/ja/3.14/library/heapq.html)
