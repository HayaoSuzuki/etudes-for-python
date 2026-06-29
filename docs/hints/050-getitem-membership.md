---
title: "050: 「inは古い扉も叩く」のヒント"
description: "__contains__も__iter__もないオブジェクトでmembership testを成立させる。"
difficulty: 4
---

# 050: 「inは古い扉も叩く」のヒント

[問題](../problems/050-getitem-membership.md) / [解答](../solutions/050-getitem-membership.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `in` は、`__contains__` がない場合に別の方法を試します。

??? tip "ヒント2"

    `__iter__` もない場合、古いシーケンスプロトコルとして `__getitem__` が使われます。

??? tip "ヒント3"

    範囲外で必ず `IndexError` を送出しないと、探索が終わりません。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#membership-test-operations)
