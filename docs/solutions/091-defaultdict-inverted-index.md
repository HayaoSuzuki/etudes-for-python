---
title: "091: 「単語は文書番号を覚えている」の解答"
description: "defaultdict(list)で単語ごとに文書番号を集める。"
difficulty: 3
---

# 091: 「単語は文書番号を覚えている」の解答

[問題](../problems/091-defaultdict-inverted-index.md) / [ヒント](../hints/091-defaultdict-inverted-index.md)

**難易度:** ☆☆☆

## 方針

単語ごとに文書番号のリストを持つ辞書を作ります。
`defaultdict(list)` を使うと、初めて出てきた単語でも空リストから始められます。

同じ文書内の重複を避けるため、文書ごとに単語の集合を作ってから文書番号を追加します。

## 実装

```python
import re
from collections import defaultdict


WORD_RE = re.compile(r"[A-Za-z0-9]+")


def document_words(text):
    return {
        match.group(0).lower()
        for match in WORD_RE.finditer(text)
    }


def build_index(documents):
    index = defaultdict(list)

    for document_id, text in enumerate(documents):
        for word in document_words(text):
            index[word].append(document_id)

    return {
        word: index[word]
        for word in sorted(index)
    }
```

## 確認

```python
assert build_index(["Red fish red bird", "Blue fish", "red blue"]) == {
    "bird": [0],
    "blue": [1, 2],
    "fish": [0, 1],
    "red": [0, 2],
}
```

## 発展

検索機能に使うなら、単語の正規化規則をそろえる必要があります。
たとえば複数形や活用形を同じ語として扱うかどうかは、検索の仕様に関わります。

## 参考

- [collections.defaultdict](https://docs.python.org/ja/3.14/library/collections.html#collections.defaultdict)
