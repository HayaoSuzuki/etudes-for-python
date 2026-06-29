---
title: "003: AEIOUだけが知っている"
description: "英語の母音の個数を数える。"
difficulty: 1
---

# 003: AEIOUだけが知っている

[ヒント](../hints/003-count-vowels.md) / [解答](../solutions/003-count-vowels.md)

**難易度:** ☆

## 問題

関数 `count_vowels(text)` を書いてください。
この関数は、文字列 `text` に含まれる英語の母音 `a`, `e`, `i`, `o`, `u` の個数を返します。

大文字の母音も同じように数えてください。

## 制約

- `text` は文字列です。
- 母音として数えるのは `a`, `e`, `i`, `o`, `u` だけです。
- `y` は母音として数えません。

## 例

```python
>>> count_vowels("hello")
2
>>> count_vowels("Python")
1
>>> count_vowels("AEIOU")
5
>>> count_vowels("")
0
```

## 発展

母音ごとの個数を辞書で返す関数も書いてください。

