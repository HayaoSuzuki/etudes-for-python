---
title: "062: 「会議は時差をまたぐ」の解答"
description: "ZoneInfoで入力時刻にタイムゾーンを付け、astimezoneで変換する。"
difficulty: 4
---

# 062: 「会議は時差をまたぐ」の解答

[問題](../problems/062-zoneinfo-meeting-time.md) / [ヒント](../hints/062-zoneinfo-meeting-time.md)

**難易度:** ☆☆☆☆

## 方針

入力の `start` は、タイムゾーン情報を含まないローカル時刻です。
まず `datetime.fromisoformat` で `datetime` に変換し、タイムゾーン情報が含まれていないことを確認します。

その後、`from_zone` の `ZoneInfo` を付け、`astimezone` で `to_zone` へ変換します。
Windowsなど、IANAタイムゾーンデータがない環境では、`tzdata` パッケージを入れて実行します。

## 実装

```python
from datetime import datetime
from zoneinfo import ZoneInfo


def convert_meeting_time(start, from_zone, to_zone):
    local_time = datetime.fromisoformat(start)
    if local_time.tzinfo is not None:
        raise ValueError("start must not include timezone information")

    source_time = local_time.replace(tzinfo=ZoneInfo(from_zone))
    converted = source_time.astimezone(ZoneInfo(to_zone))
    return converted.isoformat(timespec="minutes")
```

## 確認

```python
assert convert_meeting_time(
    "2026-07-01T09:30",
    "Asia/Tokyo",
    "America/Los_Angeles",
) == "2026-06-30T17:30-07:00"

assert convert_meeting_time(
    "2026-01-15T09:00",
    "Asia/Tokyo",
    "Europe/London",
) == "2026-01-15T00:00+00:00"

try:
    convert_meeting_time("2026-07-01T09:30+09:00", "Asia/Tokyo", "UTC")
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

現実の予定表では、存在しないローカル時刻や、夏時間の切り替えで重複するローカル時刻も問題になります。
そのような入力をどう扱うかは、アプリケーション側の仕様として決めます。

## 参考

- [zoneinfo](https://docs.python.org/ja/3.14/library/zoneinfo.html)
- [tzdata](https://pypi.org/project/tzdata/)


