---
title: "003: 「AEIOUだけが知っている」の解答"
description: "文字列を1文字ずつ調べ、英語の母音の個数を数える。"
difficulty: 1
---

# 003: 「AEIOUだけが知っている」の解答

[問題](../problems/003-count-vowels.md) / [ヒント](../hints/003-count-vowels.md)

**難易度:** ☆

## 方針

文字列を1文字ずつ調べます。
各文字を小文字にして、`aeiou` のどれかに含まれるなら個数を1増やします。

## 実装

```python
def count_vowels(text):
    count = 0
    for ch in text:
        if ch.lower() in "aeiou":
            count += 1
    return count
```

## 確認

```python
assert count_vowels("hello") == 2
assert count_vowels("Python") == 1
assert count_vowels("AEIOU") == 5
assert count_vowels("") == 0
```

## 発展

母音ごとの個数を返す場合は、辞書を使えます。
最初に各母音の個数を0にしておき、見つけた母音の値だけを増やします。

