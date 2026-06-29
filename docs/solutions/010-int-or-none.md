---
title: "010: 「42か、それ以外か」の解答"
description: "文字列を整数へ変換し、失敗したらNoneを返す。"
difficulty: 2
---

# 010: 「42か、それ以外か」の解答

[問題](../problems/010-int-or-none.md) / [ヒント](../hints/010-int-or-none.md)

**難易度:** ☆☆

## 方針

`int()` による変換を試します。
成功した場合はその値を返し、`ValueError` が出た場合だけ `None` を返します。

## 実装

```python
def int_or_none(text):
    try:
        return int(text.strip())
    except ValueError:
        return None
```

## 確認

```python
assert int_or_none("42") == 42
assert int_or_none("  -7  ") == -7
assert int_or_none("3.14") is None
assert int_or_none("hello") is None
```

## 発展

カンマ区切りの文字列に応用する場合は、項目ごとに `int_or_none()` を呼び出します。
戻り値が `None` ではないときだけ、結果のリストに追加します。

