---
title: "037: 括弧に名前をつけた日"
description: "正規表現の名前付きグループを使って日付を取り出す。"
difficulty: 3
---

# 037: 括弧に名前をつけた日

[ヒント](../hints/037-regex-named-date.md) / [解答](../solutions/037-regex-named-date.md)

**難易度:** ☆☆☆

## 問題

関数 `extract_iso_dates(text)` を書いてください。
この関数は、文字列の中から `YYYY-MM-DD` 形式の日付を取り出し、辞書のリストで返します。

返す辞書は、キー `year`、`month`、`day` を持ち、値は整数にしてください。

## 制約

- 正規表現を使ってください。
- 年は4桁です。
- 月は `01` から `12` だけを認めます。
- 日は `01` から `31` だけを認めます。
- `2026-06-30` のような日付だけを取り出し、前後に数字が続くものは取り出さないでください。
- 月ごとの日数やうるう年は考えなくてかまいません。

## 例

```python
>>> extract_iso_dates("start 2026-06-30, end 2026-07-05")
[{'year': 2026, 'month': 6, 'day': 30}, {'year': 2026, 'month': 7, 'day': 5}]
>>> extract_iso_dates("bad 2026-13-01 and 12026-06-30")
[]
```

## 参考

- [Regular expression HOWTO](https://docs.python.org/ja/3.14/howto/regex.html)

