---
title: "071: 「文字列のふりをした信号機」の解答"
description: "StrEnumで状態を表し、イベントによる状態遷移を実装する。"
difficulty: 3
---

# 071: 「文字列のふりをした信号機」の解答

[問題](../problems/071-strenum-task-state.md) / [ヒント](../hints/071-strenum-task-state.md)

**難易度:** ☆☆☆

## 方針

状態を `StrEnum` で定義し、状態遷移を辞書で表します。
`current` は最初に `TaskState` へ変換してから扱います。

## 実装

```python
from enum import StrEnum


class TaskState(StrEnum):
    TODO = "todo"
    DOING = "doing"
    DONE = "done"
    BLOCKED = "blocked"


TRANSITIONS = {
    (TaskState.TODO, "start"): TaskState.DOING,
    (TaskState.DOING, "finish"): TaskState.DONE,
    (TaskState.DOING, "block"): TaskState.BLOCKED,
    (TaskState.BLOCKED, "unblock"): TaskState.DOING,
    (TaskState.DONE, "reopen"): TaskState.TODO,
}


def next_state(current, event):
    state = TaskState(current)
    try:
        return TRANSITIONS[(state, event)]
    except KeyError as exc:
        raise ValueError(f"invalid transition: {state!s} + {event}") from exc
```

## 確認

```python
assert TaskState.TODO.value == "todo"
assert next_state("todo", "start") is TaskState.DOING
assert str(next_state(TaskState.BLOCKED, "unblock")) == "doing"
assert next_state(TaskState.DONE, "reopen") is TaskState.TODO

try:
    next_state("todo", "finish")
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

`TaskState` に、完了状態かどうかを返すメソッド `is_closed()` を追加してください。

## 参考

- [列挙型 HOWTO](https://docs.python.org/ja/3.14/howto/enum.html)

