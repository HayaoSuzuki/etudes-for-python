---
title: "027: 最後に置いた鍵が勝つ"
description: "辞書表示の評価順と重複キーの規則に合わせて値を統合する。"
difficulty: 3
---

# 027: 最後に置いた鍵が勝つ

[ヒント](../hints/027-dict-display-merge.md) / [解答](../solutions/027-dict-display-merge.md)

**難易度:** ☆☆☆

## 問題

関数 `merge_like_dict_display(parts)` を書いてください。
この関数は、辞書表示で項目や `**` 展開を左から右へ書いたときと同じ規則で、値を統合します。

`parts` の各要素は、次のどちらかです。

- `("item", key, value)`：辞書表示の `key: value` に対応します。
- `("mapping", mapping)`：辞書表示の `**mapping` に対応します。

同じキーが複数回出た場合は、後に出た値を採用してください。

## 制約

- `mapping` は辞書として扱えるオブジェクトです。
- 返り値は新しい辞書です。
- `parts` に含まれる辞書は変更しません。

## 例

```python
>>> merge_like_dict_display([
...     ("item", "color", "red"),
...     ("mapping", {"size": "M", "color": "blue"}),
...     ("item", "color", "green"),
... ])
{'color': 'green', 'size': 'M'}
>>> merge_like_dict_display([])
{}
```

## 参考

- [辞書表示](https://docs.python.org/ja/3.14/reference/expressions.html#dictionary-displays)
