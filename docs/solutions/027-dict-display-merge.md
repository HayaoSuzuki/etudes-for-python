---
title: "027: 「最後に置いた鍵が勝つ」の解答"
description: "辞書表示の評価順と重複キーの規則に合わせて値を統合する。"
difficulty: 3
---

# 027: 「最後に置いた鍵が勝つ」の解答

[問題](../problems/027-dict-display-merge.md) / [ヒント](../hints/027-dict-display-merge.md)

**難易度:** ☆☆☆

## 方針

辞書表示では、後に現れた値が前の値を置き換えます。
この規則に合わせて、`parts` を左から右へ処理し、結果の辞書へ代入していきます。

## 実装

```python
def merge_like_dict_display(parts):
    result = {}
    for part in parts:
        kind = part[0]
        if kind == "item":
            key = part[1]
            value = part[2]
            result[key] = value
        elif kind == "mapping":
            mapping = part[1]
            for key, value in mapping.items():
                result[key] = value
    return result
```

## 確認

```python
assert merge_like_dict_display([
    ("item", "color", "red"),
    ("mapping", {"size": "M", "color": "blue"}),
    ("item", "color", "green"),
]) == {"color": "green", "size": "M"}
assert merge_like_dict_display([]) == {}
```

## 発展

実際の辞書表示で、`{"x": 1, **{"x": 2}, "x": 3}` がどう評価されるかを確認してください。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#dictionary-displays)
