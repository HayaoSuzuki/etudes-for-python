---
title: "078: 「週末を数えない日付」の解答"
description: "date.fromisoformatとtimedeltaで1日ずつ進め、営業日だけを数える。"
difficulty: 4
---

# 078: 「週末を数えない日付」の解答

[問題](../problems/078-business-days.md) / [ヒント](../hints/078-business-days.md)

**難易度:** ☆☆☆☆

## 方針

日付文字列を `date` に変換し、`timedelta(days=1)` で1日ずつ進めます。
進めた日が土日でも祝日でもなければ、営業日を1日数えます。

祝日リストは先に `date` の集合に変換しておくと、判定が簡潔になります。

## 実装

```python
from datetime import date, timedelta


def is_business_day(day, holidays):
    return day.weekday() < 5 and day not in holidays


def add_business_days(start, days, holidays=()):
    if days < 0:
        raise ValueError("days must be non-negative")

    current = date.fromisoformat(start)
    holiday_dates = {date.fromisoformat(holiday) for holiday in holidays}

    remaining = days
    while remaining > 0:
        current += timedelta(days=1)
        if is_business_day(current, holiday_dates):
            remaining -= 1

    return current.isoformat()
```

## 確認

```python
assert add_business_days("2026-06-26", 1) == "2026-06-29"
assert add_business_days("2026-06-26", 1, {"2026-06-29"}) == "2026-06-30"
assert add_business_days("2026-06-30", 3) == "2026-07-03"
assert add_business_days("2026-06-30", 0) == "2026-06-30"

try:
    add_business_days("2026-06-30", -1)
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

営業日計算は地域や会社ごとの休業日に依存します。
現実のアプリケーションでは、祝日リストを外から渡す、年度ごとに読み込む、タイムゾーンを含む日時と分けて扱う、といった設計が必要になります。

## 参考

- [datetime](https://docs.python.org/ja/3.14/library/datetime.html)
