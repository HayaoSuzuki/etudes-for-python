---
title: "024: 「よく出る言葉から並べる」の解答"
description: "正規表現で単語を取り出し、Counterで頻度を数えて並べる。"
difficulty: 3
---

# 024: 「よく出る言葉から並べる」の解答

[問題](../problems/024-counter-top-words.md) / [ヒント](../hints/024-counter-top-words.md)

**難易度:** ☆☆☆

## 方針

正規表現で単語を取り出し、小文字へそろえます。
除外語も小文字の集合にしてから、対象単語だけを `Counter` で数えます。

最後に、回数の降順、単語の昇順で並べ、上位 `limit` 件だけを返します。

## 実装

```python
import re
from collections import Counter


WORD_RE = re.compile(r"[A-Za-z0-9']+")


def top_words(text, stop_words=(), limit=3):
    if limit <= 0:
        return []

    stops = {word.lower() for word in stop_words}
    words = [
        match.group(0).lower()
        for match in WORD_RE.finditer(text)
    ]
    counter = Counter(word for word in words if word not in stops)
    ranked = sorted(counter.items(), key=lambda item: (-item[1], item[0]))
    return ranked[:limit]
```

## 確認

```python
assert top_words("Red fish, blue fish. Red bird.", limit=2) == [
    ("fish", 2),
    ("red", 2),
]
assert top_words("To be, or not to be.", stop_words={"to", "or"}) == [
    ("be", 2),
    ("not", 1),
]
assert top_words("Don't stop. Don't.", limit=1) == [("don't", 2)]
assert top_words("one two", limit=0) == []
```

## 発展

`Counter.most_common()` は頻度順に取り出せます。
ただし、同じ回数の並びをアルファベット順にしたい場合は、今回のように `sorted` のキーを明示します。

## 参考

- [collections.Counter](https://docs.python.org/ja/3.14/library/collections.html#collections.Counter)




