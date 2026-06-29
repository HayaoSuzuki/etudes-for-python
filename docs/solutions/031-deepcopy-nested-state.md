---
title: "031: 「入れ子の状態は奥まで写す」の解答"
description: "deepcopyで状態全体を複製してからカード移動と履歴追加を行う。"
difficulty: 3
---

# 031: 「入れ子の状態は奥まで写す」の解答

[問題](../problems/031-deepcopy-nested-state.md) / [ヒント](../hints/031-deepcopy-nested-state.md)

**難易度:** ☆☆☆

## 方針

元の状態を変更しないため、最初に `deepcopy` で状態全体をコピーします。
以後の操作はコピー側に対して行います。

`source` 列の先頭からカードを取り出し、`target` 列の末尾へ追加します。
履歴には、移動元、移動先、カード名を文字列で残します。

## 実装

```python
from copy import deepcopy


def move_card(state, source, target):
    next_state = deepcopy(state)
    source_cards = next_state["columns"][source]

    if not source_cards:
        raise ValueError("source column is empty")

    card = source_cards.pop(0)
    next_state["columns"][target].append(card)
    next_state["history"].append(f"{source}->{target}: {card}")

    return next_state
```

## 確認

```python
state = {"columns": {"todo": ["write", "review"], "done": []}, "history": []}
next_state = move_card(state, "todo", "done")

assert next_state["columns"] == {"todo": ["review"], "done": ["write"]}
assert next_state["history"] == ["todo->done: write"]
assert state["columns"] == {"todo": ["write", "review"], "done": []}

state["columns"]["todo"].append("publish")
assert next_state["columns"]["todo"] == ["review"]

try:
    move_card({"columns": {"todo": [], "done": []}, "history": []}, "todo", "done")
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

状態が大きい場合、毎回すべてを `deepcopy` するとコストが高くなります。
変更する列と履歴だけをコピーする設計にすると、必要な範囲だけを複製できます。

## 参考

- [copy](https://docs.python.org/ja/3.14/library/copy.html)

