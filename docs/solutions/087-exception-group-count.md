---
title: "087: 「例外の束をほどく」の解答"
description: "except*でExceptionGroupを型ごとの部分グループに分ける。"
difficulty: 5
---

# 087: 「例外の束をほどく」の解答

[問題](../problems/087-exception-group-count.md) / [ヒント](../hints/087-exception-group-count.md)

**難易度:** ☆☆☆☆☆

## 方針

最初に、すべて0の辞書を作ります。
例外が空でなければ `ExceptionGroup` を送出し、`except*` で型ごとの部分グループを受け取ります。
各節では、受け取ったグループの `exceptions` の長さを記録します。

## 実装

```python
def count_exception_group(exceptions):
    counts = {"ValueError": 0, "TypeError": 0, "Other": 0}
    if exceptions == []:
        return counts

    try:
        raise ExceptionGroup("group", exceptions)
    except* ValueError as group:
        counts["ValueError"] = len(group.exceptions)
    except* TypeError as group:
        counts["TypeError"] = len(group.exceptions)
    except* Exception as group:
        counts["Other"] = len(group.exceptions)

    return counts
```

## 確認

```python
assert count_exception_group([ValueError("a"), TypeError("b"), OSError("c")]) == {
    "ValueError": 1,
    "TypeError": 1,
    "Other": 1,
}
assert count_exception_group([ValueError("a"), ValueError("b")]) == {
    "ValueError": 2,
    "TypeError": 0,
    "Other": 0,
}
assert count_exception_group([]) == {"ValueError": 0, "TypeError": 0, "Other": 0}
```

## 発展

`except* Exception` を消した場合、未処理の例外がどう伝播するかを確認してください。
`except*` は、処理しなかった部分グループを自動的に捨てません。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/compound_stmts.html#except-star)

