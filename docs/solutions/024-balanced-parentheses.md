---
title: "024: 「括弧の門番は眠らない」の解答"
description: "文字列中の丸括弧が正しく対応しているか判定する。"
difficulty: 3
---

# 024: 「括弧の門番は眠らない」の解答

[問題](../problems/024-balanced-parentheses.md) / [ヒント](../hints/024-balanced-parentheses.md)

**難易度:** ☆☆☆

## 方針

まだ閉じていない開き括弧の数を数えます。
閉じ括弧が先に出て数が負になる場合は、その時点で不正です。
最後に数が0なら、すべての開き括弧が閉じています。

## 実装

```python
def balanced_parentheses(text):
    opened = 0
    for ch in text:
        if ch == "(":
            opened += 1
        elif ch == ")":
            opened -= 1
            if opened < 0:
                return False
    return opened == 0
```

## 確認

```python
assert balanced_parentheses("(a + b) * c") is True
assert balanced_parentheses("(()())") is True
assert balanced_parentheses("())(") is False
assert balanced_parentheses("no parentheses") is True
```

## 発展

複数種類の括弧を扱う場合は、数だけでは足りません。
直近の開き括弧の種類を覚える必要があるので、リストをスタックとして使う方法を考えます。
