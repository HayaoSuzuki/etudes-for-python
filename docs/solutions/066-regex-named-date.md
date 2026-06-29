---
title: "066: 「括弧に名前をつけた日」の解答"
description: "正規表現の名前付きグループを使って日付を取り出す。"
difficulty: 3
---

# 066: 「括弧に名前をつけた日」の解答

[問題](../problems/066-regex-named-date.md) / [ヒント](../hints/066-regex-named-date.md)

**難易度:** ☆☆☆

## 方針

年、月、日を名前付きグループにします。
`finditer` で全一致箇所を走査し、各グループを整数に変換して辞書にします。

## 実装

```python
import re


DATE_RE = re.compile(
    r"(?<!\d)"
    r"(?P<year>\d{4})-"
    r"(?P<month>0[1-9]|1[0-2])-"
    r"(?P<day>0[1-9]|[12]\d|3[01])"
    r"(?!\d)"
)


def extract_iso_dates(text):
    dates = []
    for match in DATE_RE.finditer(text):
        dates.append({
            "year": int(match["year"]),
            "month": int(match["month"]),
            "day": int(match["day"]),
        })
    return dates
```

## 確認

```python
assert extract_iso_dates("start 2026-06-30, end 2026-07-05") == [
    {"year": 2026, "month": 6, "day": 30},
    {"year": 2026, "month": 7, "day": 5},
]
assert extract_iso_dates("bad 2026-13-01 and 12026-06-30") == []
```

## 発展

`datetime.date` を使って、`2026-02-31` のような実在しない日付を除外してください。

## 参考

- [Regular expression HOWTO](https://docs.python.org/ja/3.14/howto/regex.html)
