---
title: "039: 同じ顔をした別の文字"
description: "Unicode正規化で表記ゆれを比較用キーにそろえる。"
difficulty: 3
---

# 039: 同じ顔をした別の文字

[ヒント](../hints/039-unicode-canonical-key.md) / [解答](../solutions/039-unicode-canonical-key.md)

**難易度:** ☆☆☆

## 問題

関数 `canonical_key(text)` と `deduplicate_names(names)` を書いてください。

`canonical_key` は、文字列を比較用のキーに変換します。
このキーでは、互換文字の違いと大文字小文字の違いをそろえてください。

`deduplicate_names` は、名前のリストから、比較用キーが重複する要素を取り除きます。
重複した場合は、最初に出た表記を残してください。

## 制約

- `unicodedata.normalize` を使ってください。
- 戻り値では、元の表記を保ってください。

## 例

```python
>>> canonical_key("Ｃａｆｅ")
'cafe'
>>> canonical_key("Cafe\u0301") == canonical_key("café")
True
>>> deduplicate_names(["Cafe\u0301", "café", "ＣＡＦＥ", "cafe"])
['Café', 'ＣＡＦＥ']
```

## 参考

- [Unicode HOWTO](https://docs.python.org/ja/3.14/howto/unicode.html)

