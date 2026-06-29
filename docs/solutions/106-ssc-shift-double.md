---
title: "106: 「左に寄せれば二倍になる」の解答"
description: "Shift命令を使って入力値を2倍し、SSCで出力する。"
difficulty: 3
---

# 106: 「左に寄せれば二倍になる」の解答

[問題](../problems/106-ssc-shift-double.md) / [ヒント](../hints/106-ssc-shift-double.md)

**難易度:** ☆☆☆

## 方針

入力は `Read 31` で31番地に置きます。
`Shift` はAccumulatorだけを変えるので、先に `Load 31` でAccumulatorへ読み込みます。
出力する前に `Store 31` で結果をメモリへ戻します。

## 実装

```python
def double_program():
    lines = [
        "Read 31",
        "Load 31",
        "Shift 1",
        "Store 31",
        "Write 31",
        "Stop",
    ]
    program = []
    for line in lines:
        program.append(assemble_line(line))
    return program
```

## 確認

```python
assert run(double_program(), [21]) == [42]
assert run(double_program(), [-3]) == [-6]
```

## 発展

`Shift 2` は2ビット左シフトです。
Python整数では、これは4倍と同じ結果になります。

