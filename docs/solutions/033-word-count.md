---
title: "033: 「ことばたちの出席簿」の解答"
description: "単語のリストから、単語ごとの出現回数を辞書で返す。"
difficulty: 2
---

# 033: 「ことばたちの出席簿」の解答

[問題](../problems/033-word-count.md) / [ヒント](../hints/033-word-count.md)

**難易度:** ☆☆

## 方針

結果用の空の辞書を用意します。
単語を順に見て、初めて出た単語なら1、すでに出た単語なら現在の値に1を足します。

## 実装

```python
def word_count(words):
    counts = {}
    for word in words:
        if word in counts:
            counts[word] += 1
        else:
            counts[word] = 1
    return counts
```

## 確認

```python
assert word_count(["red", "blue", "red"]) == {"red": 2, "blue": 1}
assert word_count([]) == {}
assert word_count(["Python", "python"]) == {"Python": 1, "python": 1}
```

## 発展

大文字と小文字を区別しない場合は、数える前に `word.lower()` を使ってキーをそろえます。
