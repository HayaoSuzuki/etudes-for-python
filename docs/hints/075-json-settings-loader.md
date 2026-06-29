---
title: "075: 「設定はJSONから来る」のヒント"
description: "json.loadsで設定文字列を読み、必須キーと省略値を検査する。"
difficulty: 3
---

# 075: 「設定はJSONから来る」のヒント

[問題](../problems/075-json-settings-loader.md) / [解答](../solutions/075-json-settings-loader.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `json.loads(text)` は、JSON文字列をPythonの値に変換します。
    JSONオブジェクトは辞書になります。

??? tip "ヒント2"

    まず、読み込んだ値が辞書かどうかを確認します。
    リストや文字列が来た場合は、設定オブジェクトとして扱えません。

??? tip "ヒント3"

    省略できるキーは、`dict.get(key, default)` で初期値を補えます。
    ただし、補ったあとで型や値の範囲を検査します。

??? tip "ヒント4"

    `bool` は `int` のサブクラスです。
    `isinstance(True, int)` は `True` になるため、`retries` では `type(value) is int` のような検査が必要です。
