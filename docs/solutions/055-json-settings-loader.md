---
title: "055: 「設定はJSONからレポートを動かす」の解答"
description: "JSONを読み、許可キー、必須値、省略値、入れ子の型を順に検査する。"
difficulty: 4
---

# 055: 「設定はJSONからレポートを動かす」の解答

[問題](../problems/055-json-settings-loader.md) / [ヒント](../hints/055-json-settings-loader.md)

**難易度:** ☆☆☆☆

## 方針

JSON文字列をPythonの値へ変換したあと、辞書であることを確認します。
そこから、未知キー、必須キー、省略可能なキー、入れ子の辞書を順に検査します。

検査の順番を固定すると、どの入力でどのエラーを返すかが安定します。
これはテストを書きやすくするためにも有効です。

## 実装

```python
import json


ALLOWED_KEYS = {"report_name", "group_by", "min_total", "include_zero", "aliases"}
ALLOWED_GROUPS = {"item", "date"}


def load_report_settings(text):
    data = json.loads(text)

    if not isinstance(data, dict):
        raise ValueError("settings must be an object")

    unknown_keys = set(data) - ALLOWED_KEYS
    if unknown_keys:
        key = sorted(unknown_keys)[0]
        raise ValueError(f"unknown setting: {key}")

    report_name = data.get("report_name")
    if type(report_name) is not str or report_name == "":
        raise ValueError("report_name is required")

    group_by = data.get("group_by", "item")
    if group_by not in ALLOWED_GROUPS:
        raise ValueError("group_by must be item or date")

    min_total = data.get("min_total", 0)
    if type(min_total) is not int or min_total < 0:
        raise ValueError("min_total must be a non-negative int")

    include_zero = data.get("include_zero", False)
    if type(include_zero) is not bool:
        raise ValueError("include_zero must be a bool")

    aliases = data.get("aliases", {})
    if not isinstance(aliases, dict):
        raise ValueError("aliases must be an object")
    for key, value in aliases.items():
        if type(key) is not str or type(value) is not str:
            raise ValueError("aliases must map strings to strings")

    return {
        "report_name": report_name,
        "group_by": group_by,
        "min_total": min_total,
        "include_zero": include_zero,
        "aliases": dict(aliases),
    }
```

## 確認

```python
assert load_report_settings('{"report_name": "monthly"}') == {
    "report_name": "monthly",
    "group_by": "item",
    "min_total": 0,
    "include_zero": False,
    "aliases": {},
}
assert load_report_settings(
    '{"report_name": "monthly", "group_by": "date", "min_total": 1000, '
    '"include_zero": true, "aliases": {"pen": "文具"}}'
) == {
    "report_name": "monthly",
    "group_by": "date",
    "min_total": 1000,
    "include_zero": True,
    "aliases": {"pen": "文具"},
}

try:
    load_report_settings("[]")
except ValueError as error:
    assert str(error) == "settings must be an object"
else:
    raise AssertionError("ValueError was not raised")

try:
    load_report_settings('{"report_name": "monthly", "min_total": true}')
except ValueError as error:
    assert str(error) == "min_total must be a non-negative int"
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

設定項目が増えると、1つの関数に検査が集中します。
その場合は、項目ごとの検査関数を作り、どのキーをどの関数で検査するかを辞書で持つと見通しを保てます。

## 参考

- [json](https://docs.python.org/ja/3.14/library/json.html)