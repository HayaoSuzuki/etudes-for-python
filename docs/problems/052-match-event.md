---
title: "052: caseは形を見ている"
description: "構造的パターンマッチで辞書、シーケンス、ガードを使い分ける。"
difficulty: 4
---

# 052: caseは形を見ている

[ヒント](../hints/052-match-event.md) / [解答](../solutions/052-match-event.md)

**難易度:** ☆☆☆☆

## 問題

関数 `describe_event(event)` を書いてください。
この関数は、イベントを表す値を受け取り、形に応じた説明文字列を返します。

次の形を扱ってください。

- `{"type": "click", "position": (x, y)}`：`"click at x,y"` を返す
- `{"type": "key", "key": key}`：`"key key"` を返す
- `["resize", width, height]`：`width` と `height` が正の整数なら `"resize widthxheight"` を返す
- それ以外：`"unknown"` を返す

## 制約

- `match` 文を使ってください。
- `click` の座標は整数だけを受け付けます。
- `resize` の幅と高さは、正の整数だけを受け付けます。

## 例

```python
>>> describe_event({"type": "click", "position": (10, 20)})
'click at 10,20'
>>> describe_event({"type": "key", "key": "Enter"})
'key Enter'
>>> describe_event(["resize", 800, 600])
'resize 800x600'
>>> describe_event(["resize", 0, 600])
'unknown'
```

## 参考

- [`match` 文](https://docs.python.org/ja/3.14/reference/compound_stmts.html#the-match-statement)
