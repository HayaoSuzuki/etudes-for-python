---
title: "077: 出口で例外を見分ける"
description: "__exit__の返り値で特定の例外だけを抑制する。"
difficulty: 4
---

# 077: 出口で例外を見分ける

[ヒント](../hints/077-suppress-only.md) / [解答](../solutions/077-suppress-only.md)

**難易度:** ☆☆☆☆

## 問題

クラス `SuppressOnly` を書いてください。
このクラスは、指定された例外型だけを抑制するコンテキストマネージャーです。

`with SuppressOnly(ValueError):` のブロック内で `ValueError` が発生した場合は、例外を外へ出さずに処理を続けます。
指定されていない例外は、通常どおり外へ伝播させます。

## 制約

- `__enter__` と `__exit__` を実装してください。
- `__enter__` は自分自身を返してください。
- 抑制した例外オブジェクトを、属性 `suppressed` に保存してください。
- 例外が発生しなかった場合、`suppressed` は `None` のままにします。

## 例

```python
>>> with SuppressOnly(ValueError) as guard:
...     raise ValueError("bad")
>>> str(guard.suppressed)
'bad'
>>> with SuppressOnly(ValueError):
...     raise TypeError("wrong")
Traceback (most recent call last):
...
TypeError: wrong
```

## 参考

- [`with` 文](https://docs.python.org/ja/3.14/reference/compound_stmts.html#the-with-statement)

