---
title: "032: 「caseは形を見ている」の解答"
description: "構造的パターンマッチで辞書、シーケンス、ガードを使い分ける。"
difficulty: 4
---

# 032: 「caseは形を見ている」の解答

[問題](../problems/032-match-event.md) / [ヒント](../hints/032-match-event.md)

**難易度:** ☆☆☆☆

## 方針

`match` 文で、辞書パターンとシーケンスパターンを順に試します。
整数であることは `int(name)` のクラスパターンで表し、正であることはガードで確認します。

## 実装

```python
def describe_event(event):
    match event:
        case {"type": "click", "position": (int(x), int(y))}:
            return f"click at {x},{y}"
        case {"type": "key", "key": key}:
            return f"key {key}"
        case ["resize", int(width), int(height)] if width > 0 and height > 0:
            return f"resize {width}x{height}"
        case _:
            return "unknown"
```

## 確認

```python
assert describe_event({"type": "click", "position": (10, 20)}) == "click at 10,20"
assert describe_event({"type": "key", "key": "Enter"}) == "key Enter"
assert describe_event(["resize", 800, 600]) == "resize 800x600"
assert describe_event(["resize", 0, 600]) == "unknown"
assert describe_event({"type": "click", "position": ("10", 20)}) == "unknown"
```

## 発展

`{"type": "click", "position": [x, y]}` も受け付けるかどうかを決めてください。
受け付けるなら、シーケンスパターンがタプルとリストをどう扱うかを確認します。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/compound_stmts.html#the-match-statement)
