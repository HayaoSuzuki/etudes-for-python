---
title: "045: 「IDは同じ形にそろえる」の解答"
description: "UUID文字列またはUUIDオブジェクトを受け取り、標準文字列へ正規化する。"
difficulty: 3
---

# 045: 「IDは同じ形にそろえる」の解答

[問題](../problems/045-uuid-record-id.md) / [ヒント](../hints/045-uuid-record-id.md)

**難易度:** ☆☆☆

## 方針

文字列が渡された場合は `UUID(value)` で解析します。
すでに `UUID` オブジェクトならそのまま使います。

`str(uuid_obj)` で、ハイフン付きの小文字形式へ変換できます。

## 実装

```python
from uuid import UUID


def normalize_uuid(value):
    if isinstance(value, UUID):
        uuid_value = value
    elif isinstance(value, str):
        uuid_value = UUID(value)
    else:
        raise ValueError("value must be a UUID or UUID string")

    return str(uuid_value)
```

## 確認

```python
import uuid


assert normalize_uuid("550E8400E29B41D4A716446655440000") == (
    "550e8400-e29b-41d4-a716-446655440000"
)
assert normalize_uuid(uuid.UUID("550e8400-e29b-41d4-a716-446655440000")) == (
    "550e8400-e29b-41d4-a716-446655440000"
)

try:
    normalize_uuid("not-a-uuid")
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

`UUID` オブジェクトには `version` 属性があります。
バージョン4のUUIDだけを受け入れる、といった制約も追加できます。

## 参考

- [uuid](https://docs.python.org/ja/3.14/library/uuid.html)

