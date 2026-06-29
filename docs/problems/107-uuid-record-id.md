---
title: "107: IDは同じ形にそろえる"
description: "uuid.UUIDでUUID文字列を検査し、正規化した文字列へ変換する。"
difficulty: 3
---

# 107: IDは同じ形にそろえる

[ヒント](../hints/107-uuid-record-id.md) / [解答](../solutions/107-uuid-record-id.md)

**難易度:** ☆☆☆

## 問題

関数 `normalize_uuid(value)` を書いてください。

この関数は、UUIDを表す文字列または `uuid.UUID` オブジェクトを受け取り、標準的な小文字のUUID文字列を返します。

## 制約

- `uuid.UUID` を使ってください。
- `value` は文字列または `UUID` オブジェクトです。
- 不正なUUID文字列の場合は `ValueError` を送出してください。
- 戻り値は、ハイフンを含む小文字のUUID文字列です。

## 例

```python
>>> normalize_uuid("550E8400E29B41D4A716446655440000")
'550e8400-e29b-41d4-a716-446655440000'
>>> import uuid
>>> normalize_uuid(uuid.UUID("550e8400-e29b-41d4-a716-446655440000"))
'550e8400-e29b-41d4-a716-446655440000'
```

## 発展

UUIDのバージョンを検査する引数を追加してください。

## 参考

- [uuid](https://docs.python.org/ja/3.14/library/uuid.html)
