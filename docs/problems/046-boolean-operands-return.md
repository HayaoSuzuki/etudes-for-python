---
title: "046: 偽ならそのまま帰る"
description: "andとorが真偽値ではなく評価された値を返すことを確かめる。"
difficulty: 3
---

# 046: 偽ならそのまま帰る

[ヒント](../hints/046-boolean-operands-return.md) / [解答](../solutions/046-boolean-operands-return.md)

**難易度:** ☆☆☆

## 問題

関数 `boolean_operands(a, b)` を書いてください。
この関数は、`a` と `b` を受け取り、次の3つの値を辞書で返します。

- キー `"or"`：`a or b` の結果
- キー `"and"`：`a and b` の結果
- キー `"not"`：`not a` の結果

`and` と `or` は、返り値を `bool` に変換しないでください。
Pythonの式そのものが返す値を、そのまま返してください。

## 制約

- `a` と `b` は任意のPythonオブジェクトです。
- 関数内で `bool()` を呼び出してはいけません。
- `not` の結果だけは、Pythonの仕様どおり `bool` になります。

## 例

```python
>>> boolean_operands("", "fallback")
{'or': 'fallback', 'and': '', 'not': True}
>>> boolean_operands("name", "fallback")
{'or': 'name', 'and': 'fallback', 'not': False}
>>> boolean_operands([], [1, 2])
{'or': [1, 2], 'and': [], 'not': True}
```

## 参考

- [ブール演算](https://docs.python.org/ja/3.14/reference/expressions.html#boolean-operations)
