---
title: "037: 「零時をまたぐ分針」の解答"
description: "HH:MM形式の時刻から、次の時刻までの分数を求める。"
difficulty: 3
---

# 037: 「零時をまたぐ分針」の解答

[問題](../problems/037-minutes-until.md) / [ヒント](../hints/037-minutes-until.md)

**難易度:** ☆☆☆

## 方針

`HH:MM` を、0時からの分数に変換します。
たとえば `09:15` は `9 * 60 + 15` です。
差が負になった場合は、日付をまたいだものとして24時間ぶんを足します。

## 実装

```python
def minutes_until(start, end):
    start_hour, start_minute = start.split(":")
    end_hour, end_minute = end.split(":")

    start_total = int(start_hour) * 60 + int(start_minute)
    end_total = int(end_hour) * 60 + int(end_minute)

    minutes = end_total - start_total
    if minutes < 0:
        minutes += 24 * 60
    return minutes
```

## 確認

```python
assert minutes_until("09:15", "10:00") == 45
assert minutes_until("23:50", "00:10") == 20
assert minutes_until("09:00", "09:00") == 0
```

## 発展

`split(":")` と `int()` は、`"9:05"` でも同じように使えます。
表示を常に2桁にしたい場合だけ、別途整形が必要です。
