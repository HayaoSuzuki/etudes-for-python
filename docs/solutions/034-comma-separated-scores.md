---
title: "034: 「カンマの向こうに点がある」の解答"
description: "カンマ区切りの文字列から、整数のリストを作る。"
difficulty: 2
---

# 034: 「カンマの向こうに点がある」の解答

[問題](../problems/034-comma-separated-scores.md) / [ヒント](../hints/034-comma-separated-scores.md)

**難易度:** ☆☆

## 方針

空文字列の場合は、すぐに空リストを返します。
それ以外では、カンマで分けた各項目を前後の空白を取り除いてから整数に変換します。

## 実装

```python
def parse_scores(line):
    if line == "":
        return []

    scores = []
    for item in line.split(","):
        scores.append(int(item.strip()))
    return scores
```

## 確認

```python
assert parse_scores("80,90,70") == [80, 90, 70]
assert parse_scores(" 100, 95, 88 ") == [100, 95, 88]
assert parse_scores("") == []
```

## 発展

不正な項目を無視するには、`int()` の変換を `try` 文の中で行います。
この考え方は、次の問題で扱います。
