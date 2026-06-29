---
title: "002: 「先立つもの」の解答"
description: "時刻を整数に変換し、ソート済み区間を走査して空き時間を作る。"
difficulty: 1
---

# 002: 「先立つもの」の解答

[問題](../problems/002-minutes-until.md) / [ヒント](../hints/002-minutes-until.md)

**難易度:** ☆
## 方針

時刻文字列を分数に変換すると、予定は数直線上の区間として扱えます。
予定を開始時刻で並べ替え、現在時刻 `cursor` から次の予定の開始時刻までを空き時間として取り出します。

予定の開始時刻が `cursor` より前なら、直前の予定と重なっています。
この場合は空き時間を作らず、例外を送出します。

## 実装

```python
def to_minutes(time_text):
    hour_text, minute_text = time_text.split(":")
    return int(hour_text) * 60 + int(minute_text)


def to_time(minutes):
    hour, minute = divmod(minutes, 60)
    return f"{hour:02d}:{minute:02d}"


def free_slots(events, day_start, day_end):
    busy = sorted((to_minutes(start), to_minutes(end)) for start, end in events)
    cursor = to_minutes(day_start)
    limit = to_minutes(day_end)
    slots = []

    for start, end in busy:
        if start < cursor:
            raise ValueError("events overlap")
        if cursor < start:
            slots.append((to_time(cursor), to_time(start), start - cursor))
        cursor = end

    if cursor < limit:
        slots.append((to_time(cursor), to_time(limit), limit - cursor))

    return slots
```

## 確認

```python
events = [("13:00", "14:00"), ("09:30", "10:15"), ("11:00", "12:00")]
assert free_slots(events, "09:00", "15:00") == [
    ("09:00", "09:30", 30),
    ("10:15", "11:00", 45),
    ("12:00", "13:00", 60),
    ("14:00", "15:00", 60),
]
assert free_slots([], "09:00", "10:00") == [("09:00", "10:00", 60)]

try:
    free_slots([("09:00", "10:00"), ("09:30", "11:00")], "09:00", "12:00")
except ValueError as exc:
    assert str(exc) == "events overlap"
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

時間帯からはみ出す予定を扱うなら、各予定の開始時刻に `max(start, day_start)`、終了時刻に `min(end, day_end)` を適用します。
切り詰めたあとで空になる予定は、調べる時間帯と交差していません。