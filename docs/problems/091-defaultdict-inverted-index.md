---
title: "091: 単語は文書番号を覚えている"
description: "defaultdictで単語から文書番号への転置インデックスを作る。"
difficulty: 3
---

# 091: 単語は文書番号を覚えている

[ヒント](../hints/091-defaultdict-inverted-index.md) / [解答](../solutions/091-defaultdict-inverted-index.md)

**難易度:** ☆☆☆

## 問題

関数 `build_index(documents)` を書いてください。

`documents` は文書文字列のリストです。
戻り値は、単語から、その単語を含む文書番号のリストへの辞書です。
文書番号は0から始まるインデックスです。

## 制約

- `collections.defaultdict` を使ってください。
- 単語は、英数字が連続したものとします。
- 大文字と小文字は区別しません。
- 1つの文書に同じ単語が複数回出ても、その文書番号は1回だけ入れてください。
- 各単語の文書番号リストは昇順にしてください。
- 戻り値は通常の `dict` にしてください。

## 例

```python
>>> build_index(["Red fish red bird", "Blue fish", "red blue"])
{'bird': [0], 'blue': [1, 2], 'fish': [0, 1], 'red': [0, 2]}
```

## 発展

文書番号だけでなく、文書内の出現位置も保存してください。

## 参考

- [collections.defaultdict](https://docs.python.org/ja/3.14/library/collections.html#collections.defaultdict)
