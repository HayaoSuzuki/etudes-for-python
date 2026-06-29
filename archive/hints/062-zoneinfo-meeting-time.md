---
title: "062: 「会議は時差をまたぐ」のヒント"
description: "zoneinfoでローカル時刻を別のタイムゾーンへ変換する。"
difficulty: 4
---

# 062: 「会議は時差をまたぐ」のヒント

[問題](../problems/062-zoneinfo-meeting-time.md) / [解答](../solutions/062-zoneinfo-meeting-time.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `datetime.fromisoformat` は、ISO形式の文字列から `datetime` オブジェクトを作ります。
    入力にタイムゾーン情報があるかどうかは `dt.tzinfo` で確認できます。

??? tip "ヒント2"

    タイムゾーン名からタイムゾーン情報を作るには、`ZoneInfo("Asia/Tokyo")` のようにします。

??? tip "ヒント3"

    入力時刻は `from_zone` のローカル時刻です。
    `replace(tzinfo=ZoneInfo(from_zone))` で、そのタイムゾーンの時刻として扱えます。

??? tip "ヒント4"

    別のタイムゾーンへ変換するには `astimezone(ZoneInfo(to_zone))` を使います。
    出力は `isoformat(timespec="minutes")` で分までにそろえられます。

