---
title: "031: 入れ子の状態は奥まで写す"
description: "copy.deepcopyで入れ子の辞書とリストを複製し、元の状態を変更しない。"
difficulty: 3
---

# 031: 入れ子の状態は奥まで写す

[ヒント](../hints/031-deepcopy-nested-state.md) / [解答](../solutions/031-deepcopy-nested-state.md)

**難易度:** ☆☆☆

## 問題

関数 `move_card(state, source, target)` を書いてください。

`state` は、カードを列ごとに持つカンバンボードの状態です。
`move_card` は、`source` 列の先頭カードを `target` 列の末尾へ移動した新しい状態を返します。
元の `state` は変更しないでください。

## 制約

- `copy.deepcopy` を使ってください。
- `state` は、キー `columns` と `history` を持つ辞書です。
- `state["columns"]` は、列名をキー、カード名のリストを値に持つ辞書です。
- `source` 列が空の場合は `ValueError` を送出してください。
- 新しい状態の `history` には、`"source->target: card"` 形式の文字列を追加してください。
- 戻り値の入れ子のリストは、元の状態と共有しないでください。

## 例

```python
>>> state = {"columns": {"todo": ["write", "review"], "done": []}, "history": []}
>>> next_state = move_card(state, "todo", "done")
>>> next_state["columns"]
{'todo': ['review'], 'done': ['write']}
>>> next_state["history"]
['todo->done: write']
>>> state["columns"]
{'todo': ['write', 'review'], 'done': []}
```

## 発展

任意の位置にあるカードを移動できるようにしてください。

## 参考

- [copy](https://docs.python.org/ja/3.14/library/copy.html)

