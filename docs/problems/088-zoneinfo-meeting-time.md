---
title: "088: 会議は時差をまたぐ"
description: "zoneinfoでローカル時刻を別のタイムゾーンへ変換する。"
difficulty: 4
---

# 088: 会議は時差をまたぐ

[ヒント](../hints/088-zoneinfo-meeting-time.md) / [解答](../solutions/088-zoneinfo-meeting-time.md)

**難易度:** ☆☆☆☆

## 問題

関数 `convert_meeting_time(start, from_zone, to_zone)` を書いてください。

この関数は、あるタイムゾーンのローカル時刻として渡された会議開始時刻を、別のタイムゾーンの時刻へ変換します。

## 制約

- `datetime` と `zoneinfo.ZoneInfo` を使ってください。
- `start` はタイムゾーン情報を含まないISO形式の文字列です。
- `from_zone` と `to_zone` は、`Asia/Tokyo` のようなIANAタイムゾーン名です。
- `start` にタイムゾーン情報が含まれている場合は `ValueError` を送出してください。
- 戻り値は、変換後の時刻を `YYYY-MM-DDTHH:MM±HH:MM` 形式の文字列にしてください。
- 夏時間の有無は `zoneinfo` に任せてください。
- IANAタイムゾーンデータがない環境では、`tzdata` パッケージが必要になることがあります。

## 例

```python
>>> convert_meeting_time("2026-07-01T09:30", "Asia/Tokyo", "America/Los_Angeles")
'2026-06-30T17:30-07:00'
>>> convert_meeting_time("2026-01-15T09:00", "Asia/Tokyo", "Europe/London")
'2026-01-15T00:00+00:00'
```

## 発展

変換後の曜日も返すようにしてください。

## 参考

- [zoneinfo](https://docs.python.org/ja/3.14/library/zoneinfo.html)
- [tzdata](https://pypi.org/project/tzdata/)

