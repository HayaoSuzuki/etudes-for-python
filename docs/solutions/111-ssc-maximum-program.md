---
title: "111: 「最大値を探す小さな計算機」の解答"
description: "SSCアセンブリで2つの入力の最大値を求める。"
difficulty: 5
---

# 111: 「最大値を探す小さな計算機」の解答

[問題](../problems/111-ssc-maximum-program.md) / [ヒント](../hints/111-ssc-maximum-program.md)

**難易度:** ☆☆☆☆☆

## 方針

`a - b` が正なら、`a` が大きい値です。
正でなければ、同じか `b` が大きいので、`b` を答えにします。
SSCには無条件分岐がないため、定数1をAccumulatorに読み込んでから `Jump` します。

## 実装

```python
def maximum_program():
    return [
        "Read a",
        "Read b",
        "Load a",
        "Sub b",
        "Jump use_a",
        "Load b",
        "Store answer",
        "Load one",
        "Jump output",
        "use_a: Load a",
        "Store answer",
        "output: Write answer",
        "Stop",
        "a: Data 0",
        "b: Data 0",
        "answer: Data 0",
        "one: Data 1",
    ]


def max_with_ssc(a, b):
    program = assemble_program(maximum_program())
    outputs = run(program, [a, b])
    return outputs[0]
```

## 確認

```python
assert max_with_ssc(7, 9) == 9
assert max_with_ssc(12, 4) == 12
assert max_with_ssc(5, 5) == 5
assert max_with_ssc(-3, -8) == -3
```

## 発展

3つの入力に拡張するには、まず2つの最大値を求め、その結果と3つ目の値をもう一度比較します。
同じ比較ブロックをどう再利用するかが課題になります。

