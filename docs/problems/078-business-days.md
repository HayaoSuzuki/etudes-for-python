---
title: "078: 週末を数えない日付"
description: "datetime.dateで日付を扱い、土日と祝日を除いて営業日を進める。"
difficulty: 4
---

# 078: 週末を数えない日付

[ヒント](../hints/078-business-days.md) / [解答](../solutions/078-business-days.md)

**難易度:** ☆☆☆☆

## 問題

関数 `add_business_days(start, days, holidays=())` を書いてください。

この関数は、開始日から指定された営業日数だけ後の日付を返します。
営業日は、土曜日、日曜日、祝日リストに含まれる日付を除いた日です。

## 制約

- `datetime.date` を使ってください。
- `start` は `YYYY-MM-DD` 形式の文字列です。
- `holidays` は `YYYY-MM-DD` 形式の文字列のイテラブルです。
- `days` は0以上の整数です。
- `days` が負の場合は `ValueError` を送出してください。
- 開始日は数えません。次の日から数え始めます。
- `days` が0の場合は、開始日をそのまま返してください。
- 戻り値は `YYYY-MM-DD` 形式の文字列です。

## 例

```python
>>> add_business_days("2026-06-26", 1)
'2026-06-29'
>>> add_business_days("2026-06-26", 1, {"2026-06-29"})
'2026-06-30'
>>> add_business_days("2026-06-30", 3)
'2026-07-03'
```

## 発展

2つの日付の間に含まれる営業日数を数える関数も書いてください。

## 参考

- [datetime](https://docs.python.org/ja/3.14/library/datetime.html)
