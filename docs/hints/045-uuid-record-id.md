---
title: "045: 「IDは同じ形にそろえる」のヒント"
description: "uuid.UUIDでUUID文字列を検査し、正規化した文字列へ変換する。"
difficulty: 3
---

# 045: 「IDは同じ形にそろえる」のヒント

[問題](../problems/045-uuid-record-id.md) / [解答](../solutions/045-uuid-record-id.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `uuid.UUID` は、UUID文字列を解析してUUIDオブジェクトを作ります。
    不正な文字列では `ValueError` が送出されます。

??? tip "ヒント2"

    すでに `UUID` オブジェクトが渡された場合は、そのまま使えます。

??? tip "ヒント3"

    `str(uuid_obj)` は、ハイフン付きの小文字形式を返します。

??? tip "ヒント4"

    文字列と `UUID` 以外の型をどう扱うかも決めておくと、関数の失敗が明確になります。
    今回は `ValueError` として扱えます。

