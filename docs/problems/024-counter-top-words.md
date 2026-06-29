---
title: "024: よく出る言葉から並べる"
description: "collections.Counterで単語の出現回数を数え、頻度順に上位語を返す。"
difficulty: 3
---

# 024: よく出る言葉から並べる

[ヒント](../hints/024-counter-top-words.md) / [解答](../solutions/024-counter-top-words.md)

**難易度:** ☆☆☆

## 問題

関数 `top_words(text, stop_words=(), limit=3)` を書いてください。

この関数は、英文から単語を取り出し、出現回数の多い順に上位の単語を返します。

## 制約

- `collections.Counter` を使ってください。
- 単語は、英数字とアポストロフィ `'` が連続したものとします。
- 大文字と小文字は区別しません。
- `stop_words` に含まれる単語は結果から除外してください。
- 同じ回数の単語は、アルファベット順に並べてください。
- 戻り値は `(word, count)` のタプルのリストです。
- `limit` が0以下の場合は空のリストを返してください。

## 例

```python
>>> top_words("Red fish, blue fish. Red bird.", limit=2)
[('fish', 2), ('red', 2)]
>>> top_words("To be, or not to be.", stop_words={"to", "or"})
[('be', 2), ('not', 1)]
>>> top_words("Don't stop. Don't.", limit=1)
[("don't", 2)]
```

## 発展

日本語のように空白で単語が分かれない文章を扱う場合、どの単位で数えるべきか考えてください。

## 参考

- [collections.Counter](https://docs.python.org/ja/3.14/library/collections.html#collections.Counter)


