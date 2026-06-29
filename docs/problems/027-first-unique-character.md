---
title: "027: 一度だけ現れる声"
description: "文字列の中で最初に一度だけ現れる文字を探す。"
difficulty: 3
---

# 027: 一度だけ現れる声

[ヒント](../hints/027-first-unique-character.md) / [解答](../solutions/027-first-unique-character.md)

**難易度:** ☆☆☆

## 問題

関数 `first_unique_char(text)` を書いてください。
この関数は、文字列 `text` の中で最初に一度だけ現れる文字を返します。
そのような文字がない場合は `None` を返してください。

大文字と小文字は区別します。
空白も1つの文字として扱います。

## 制約

- `text` は文字列です。
- 返すのは1文字の文字列、または `None` です。

## 例

```python
>>> first_unique_char("swiss")
'w'
>>> first_unique_char("aabbc")
'c'
>>> first_unique_char("aabb") is None
True
>>> first_unique_char("Aa")
'A'
```

## 発展

大文字と小文字を区別しない版も書いてください。

