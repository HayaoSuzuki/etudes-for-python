---
title: "049: スライスは切らずに渡される"
description: "__getitem__に渡されるsliceオブジェクトとタプル添字を観察する。"
difficulty: 4
---

# 049: スライスは切らずに渡される

[ヒント](../hints/049-slice-recorder.md) / [解答](../solutions/049-slice-recorder.md)

**難易度:** ☆☆☆☆

## 問題

クラス `SliceRecorder` を書いてください。
このクラスのインスタンスに添字やスライスを使うと、`__getitem__` に渡されたキーを観察しやすい形で返します。

返り値は次の規則にしてください。

- 通常の添字は、その値をそのまま返します。
- `slice` オブジェクトは `("slice", start, stop, step)` のタプルにします。
- カンマ区切りの添字はタプルとして受け取り、各要素に同じ変換を適用します。

## 制約

- `__getitem__` を実装してください。
- `slice` の `start`、`stop`、`step` が省略された場合は `None` として扱います。
- 実際にシーケンスから値を取り出す必要はありません。

## 例

```python
>>> recorder = SliceRecorder()
>>> recorder[3]
3
>>> recorder[1:5:2]
('slice', 1, 5, 2)
>>> recorder[:3]
('slice', None, 3, None)
>>> recorder[1:4, "x", ::-1]
(('slice', 1, 4, None), 'x', ('slice', None, None, -1))
```

## 参考

- [スライス](https://docs.python.org/ja/3.14/reference/expressions.html#slicings)
