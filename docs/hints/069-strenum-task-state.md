---
title: "069: 「文字列のふりをした信号機」のヒント"
description: "StrEnumで状態を表し、イベントによる状態遷移を実装する。"
difficulty: 3
---

# 069: 「文字列のふりをした信号機」のヒント

[問題](../problems/069-strenum-task-state.md) / [解答](../solutions/069-strenum-task-state.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `StrEnum` を継承すると、列挙子を文字列のように扱えます。

??? tip "ヒント2"

    `TaskState(current)` と書くと、文字列から対応する列挙子に変換できます。
    対応する値がない場合は `ValueError` になります。

??? tip "ヒント3"

    状態遷移表は、`(状態, イベント)` をキーにした辞書で表せます。

??? tip "ヒント4"

    不正な遷移で `KeyError` が出たら、利用者に見せる例外として `ValueError` に変換します。
