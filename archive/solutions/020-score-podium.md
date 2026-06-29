---
title: "020: 「名前順では勝てない表彰台」の解答"
description: "名前と点数の組を、点数順と名前順で並べる。"
difficulty: 3
---

# 020: 「名前順では勝てない表彰台」の解答

[問題](../problems/020-score-podium.md) / [ヒント](../hints/020-score-podium.md)

**難易度:** ☆☆☆

## 方針

並べ替え用のキーとして、`(-score, name)` を使います。
点数は負にすることで、点数が高いほど小さい値として並びます。
そのあと、先頭から `limit` 件だけを取り出し、名前だけを返します。

## 実装

```python
def podium(records, limit=3):
    ordered = sorted(records, key=lambda record: (-record[1], record[0]))
    result = []
    for name, score in ordered[:limit]:
        result.append(name)
    return result
```

## 確認

```python
assert podium([("Ada", 90), ("Bob", 95), ("Cyd", 95), ("Dee", 80)]) == ["Bob", "Cyd", "Ada"]
assert podium([("Mika", 10), ("Aki", 10)], 1) == ["Aki"]
assert podium([], 3) == []
```

## 発展

タプルのまま返す場合は、`ordered[:limit]` をそのまま返せます。
名前だけを取り出すためのループが不要になります。

