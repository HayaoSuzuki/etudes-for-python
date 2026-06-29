---
title: "047: 「真ん中は一度だけ呼ばれる」の解答"
description: "比較の連鎖で中央の式が一度だけ評価されることを使う。"
difficulty: 3
---

# 047: 「真ん中は一度だけ呼ばれる」の解答

[問題](../problems/047-comparison-chain-once.md) / [ヒント](../hints/047-comparison-chain-once.md)

**難易度:** ☆☆☆

## 方針

比較連鎖をそのまま使います。
`low < get_value() <= high` では、`get_value()` の結果が中央の値として一度だけ評価されます。

## 実装

```python
def between_once(get_value, low, high):
    return low < get_value() <= high
```

## 確認

```python
calls = []
def read_value():
    calls.append("called")
    return 5

assert between_once(read_value, 1, 5) is True
assert calls == ["called"]
assert between_once(lambda: 0, 1, 5) is False
```

## 発展

`low < get_value() > high` も文法としては正しい比較連鎖です。
この式が何を判定しているかを、リファレンスの定義に沿って説明してください。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#comparisons)
