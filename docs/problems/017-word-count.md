---
title: "017: ことばたちの出席簿"
description: "単語のリストから、単語ごとの出現回数を辞書で返す。"
difficulty: 2
---

# 017: ことばたちの出席簿

[ヒント](../hints/017-word-count.md) / [解答](../solutions/017-word-count.md)

**難易度:** ☆☆

## 問題

関数 `word_count(words)` を書いてください。
この関数は、単語のリスト `words` を受け取り、単語ごとの出現回数を辞書で返します。

## 制約

- `words` は文字列のリストです。
- 大文字と小文字は区別します。
- 単語の前後の空白処理は、この問題では扱いません。

## 例

```python
>>> word_count(["red", "blue", "red"])
{'red': 2, 'blue': 1}
>>> word_count([])
{}
>>> word_count(["Python", "python"])
{'Python': 1, 'python': 1}
```

## 発展

大文字と小文字を区別せずに数える版も書いてください。

