---
title: "055: 設定はJSONから来る"
description: "json.loadsで設定文字列を読み、必須キーと省略値を検査する。"
difficulty: 3
---

# 055: 設定はJSONから来る

[ヒント](../hints/055-json-settings-loader.md) / [解答](../solutions/055-json-settings-loader.md)

**難易度:** ☆☆☆

## 問題

関数 `load_settings(text)` を書いてください。

この関数は、JSON文字列で渡された設定を読み、プログラム内で使う設定辞書に変換します。

扱う設定項目は次の3つです。

- `name`: 必須。空でない文字列
- `retries`: 省略可。0以上の整数。省略時は `3`
- `debug`: 省略可。真偽値。省略時は `False`

## 制約

- `json.loads` を使ってください。
- JSON全体はオブジェクトでなければなりません。
- 不明なキーが含まれている場合は `ValueError` を送出してください。
- `name` がない場合、または空文字列の場合は `ValueError` を送出してください。
- `retries` に `bool` を受け入れてはいけません。
- 検査に成功した場合は、キー `name`、`retries`、`debug` を持つ辞書を返してください。

## 例

```python
>>> load_settings('{"name": "worker"}')
{'name': 'worker', 'retries': 3, 'debug': False}
>>> load_settings('{"name": "worker", "retries": 0, "debug": true}')
{'name': 'worker', 'retries': 0, 'debug': True}
>>> load_settings('[]')
Traceback (most recent call last):
...
ValueError: settings must be an object
```

## 発展

`mode` のような列挙型の設定を追加し、許可された値だけを受け入れてください。

## 参考

- [json](https://docs.python.org/ja/3.14/library/json.html)

