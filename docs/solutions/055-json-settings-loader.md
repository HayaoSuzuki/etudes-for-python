---
title: "055: 「設定はJSONから来る」の解答"
description: "json.loadsで辞書を作り、キー、型、省略値を順に検査する。"
difficulty: 3
---

# 055: 「設定はJSONから来る」の解答

[問題](../problems/055-json-settings-loader.md) / [ヒント](../hints/055-json-settings-loader.md)

**難易度:** ☆☆☆

## 方針

最初にJSON文字列をPythonの値へ変換します。
その値が辞書であることを確認してから、不明なキー、必須キー、省略値つきのキーを順に検査します。

`bool` は `int` のサブクラスなので、`retries` では `isinstance(value, int)` ではなく `type(value) is int` で検査します。

## 実装

```python
import json


ALLOWED_KEYS = {"name", "retries", "debug"}


def load_settings(text):
    data = json.loads(text)

    if not isinstance(data, dict):
        raise ValueError("settings must be an object")

    unknown_keys = set(data) - ALLOWED_KEYS
    if unknown_keys:
        key = sorted(unknown_keys)[0]
        raise ValueError(f"unknown setting: {key}")

    name = data.get("name")
    if type(name) is not str or name == "":
        raise ValueError("name is required")

    retries = data.get("retries", 3)
    if type(retries) is not int or retries < 0:
        raise ValueError("retries must be a non-negative int")

    debug = data.get("debug", False)
    if type(debug) is not bool:
        raise ValueError("debug must be a bool")

    return {
        "name": name,
        "retries": retries,
        "debug": debug,
    }
```

## 確認

```python
assert load_settings('{"name": "worker"}') == {
    "name": "worker",
    "retries": 3,
    "debug": False,
}
assert load_settings('{"name": "worker", "retries": 0, "debug": true}') == {
    "name": "worker",
    "retries": 0,
    "debug": True,
}

try:
    load_settings("[]")
except ValueError as error:
    assert str(error) == "settings must be an object"
else:
    raise AssertionError("ValueError was not raised")

try:
    load_settings('{"name": "worker", "retries": true}')
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

設定項目が増えたら、項目ごとの検査関数を辞書にまとめると、条件分岐の見通しを保ちやすくなります。

## 参考

- [json](https://docs.python.org/ja/3.14/library/json.html)

