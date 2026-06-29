---
title: "071: 「同じ顔をした別の文字」の解答"
description: "Unicode正規化とcasefoldで、表記ゆれを比較用キーに変換する。"
difficulty: 3
---

# 071: 「同じ顔をした別の文字」の解答

[問題](../problems/071-unicode-canonical-key.md) / [ヒント](../hints/071-unicode-canonical-key.md)

**難易度:** ☆☆☆

## 方針

比較用キーでは、まず `NFKC` で正規化し、そのあと `casefold` で大小文字の差をそろえます。
重複除去では、比較用キーだけを記録し、返す値は入力の表記を残します。

## 実装

```python
import unicodedata


def canonical_key(text):
    return unicodedata.normalize("NFKC", text).casefold()


def deduplicate_names(names):
    seen = set()
    result = []

    for name in names:
        key = canonical_key(name)
        if key in seen:
            continue
        seen.add(key)
        result.append(name)

    return result
```

## 確認

```python
assert canonical_key("Ｃａｆｅ") == "cafe"
assert canonical_key("Cafe\u0301") == canonical_key("café")
assert deduplicate_names(["Cafe\u0301", "café", "ＣＡＦＥ", "cafe"]) == [
    "Cafe\u0301",
    "ＣＡＦＥ",
]
```

## 発展

アクセントの違いも無視したい場合、どの正規化形式とどの追加処理が必要かを調べてください。

## 参考

- [Unicode HOWTO](https://docs.python.org/ja/3.14/howto/unicode.html)
