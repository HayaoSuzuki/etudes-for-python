---
title: "069: 文字列のふりをした信号機"
description: "StrEnumで状態を表し、イベントによる状態遷移を実装する。"
difficulty: 3
---

# 069: 文字列のふりをした信号機

[ヒント](../hints/069-strenum-task-state.md) / [解答](../solutions/069-strenum-task-state.md)

**難易度:** ☆☆☆

## 問題

`TaskState` と関数 `next_state(current, event)` を書いてください。

`TaskState` は、タスクの状態を表す列挙型です。
状態は次の4つです。

- `TODO`
- `DOING`
- `DONE`
- `BLOCKED`

値はそれぞれ、文字列 `"todo"`、`"doing"`、`"done"`、`"blocked"` にしてください。

`next_state` は、現在の状態とイベント名を受け取り、次の状態を返します。

## 状態遷移

| 現在の状態 | イベント | 次の状態 |
|---|---|---|
| `todo` | `start` | `doing` |
| `doing` | `finish` | `done` |
| `doing` | `block` | `blocked` |
| `blocked` | `unblock` | `doing` |
| `done` | `reopen` | `todo` |

## 制約

- `enum.StrEnum` を使ってください。
- `current` には `TaskState` または文字列を渡せるようにしてください。
- 不正な状態または遷移には `ValueError` を送出してください。

## 例

```python
>>> TaskState.TODO.value
'todo'
>>> next_state("todo", "start")
<TaskState.DOING: 'doing'>
>>> str(next_state(TaskState.BLOCKED, "unblock"))
'doing'
```

## 参考

- [列挙型 HOWTO](https://docs.python.org/ja/3.14/howto/enum.html)
