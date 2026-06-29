---
title: "055: 設定はJSONからレポートを動かす"
description: "JSON設定を読み、既定値、未知キー、型、入れ子の辞書を検査する。"
difficulty: 4
---

# 055: 設定はJSONからレポートを動かす

[ヒント](../hints/055-json-settings-loader.md) / [解答](../solutions/055-json-settings-loader.md)

**難易度:** ☆☆☆☆

## 問題

関数 `load_report_settings(text)` を書いてください。
この関数は、JSON文字列で渡された売上レポート設定を読み、プログラム内で使う設定辞書に変換します。

扱う設定項目は次の5つです。

- `report_name`：必須。空でない文字列
- `group_by`：省略可。`"item"` または `"date"`。省略時は `"item"`
- `min_total`：省略可。0以上の整数。省略時は `0`
- `include_zero`：省略可。真偽値。省略時は `False`
- `aliases`：省略可。文字列から文字列への辞書。省略時は空の辞書

検査に成功した場合は、この5つのキーをすべて持つ辞書を返してください。

## 制約

- `json.loads` を使ってください。
- JSON全体はオブジェクトでなければなりません。
- 不明なキーが含まれている場合は `ValueError` を送出してください。
- `min_total` に `bool` を受け入れてはいけません。
- `aliases` のキーと値は、どちらも文字列でなければなりません。

## 例

```python
>>> load_report_settings('{"report_name": "monthly"}')
{'report_name': 'monthly', 'group_by': 'item', 'min_total': 0, 'include_zero': False, 'aliases': {}}
>>> load_report_settings('{"report_name": "monthly", "group_by": "date", "min_total": 1000, "include_zero": true, "aliases": {"pen": "文具"}}')
{'report_name': 'monthly', 'group_by': 'date', 'min_total': 1000, 'include_zero': True, 'aliases': {'pen': '文具'}}
>>> load_report_settings('[]')
Traceback (most recent call last):
...
ValueError: settings must be an object
```

## 発展

`sort_by` を追加し、`"name"`、`"total"`、`"count"` のいずれかだけを受け入れるようにしてください。

## 参考

- [json](https://docs.python.org/ja/3.14/library/json.html)