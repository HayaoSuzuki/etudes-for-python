---
title: "042: 括弧の門番は眠らない"
description: "文字列中の丸括弧が正しく対応しているか判定する。"
difficulty: 3
---

# 042: 括弧の門番は眠らない

[ヒント](../hints/042-balanced-parentheses.md) / [解答](../solutions/042-balanced-parentheses.md)

**難易度:** ☆☆☆

## 問題

関数 `balanced_parentheses(text)` を書いてください。
この関数は、文字列 `text` に含まれる丸括弧 `(` と `)` が正しく対応している場合に `True`、そうでない場合に `False` を返します。

丸括弧以外の文字は無視してください。

## 制約

- `text` は文字列です。
- 扱う括弧は `(` と `)` だけです。
- 空文字列は正しく対応しているものとします。

## 例

```python
>>> balanced_parentheses("(a + b) * c")
True
>>> balanced_parentheses("(()())")
True
>>> balanced_parentheses("())(")
False
>>> balanced_parentheses("no parentheses")
True
```

## 発展

角括弧 `[]` と波括弧 `{}` も扱う版を考えてください。
