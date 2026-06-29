---
title: "060: 左に寄せれば二倍になる"
description: "Shift命令を使って入力値を2倍し、SSCで出力する。"
difficulty: 3
---

# 060: 左に寄せれば二倍になる

[ヒント](../hints/060-ssc-shift-double.md) / [解答](../solutions/060-ssc-shift-double.md)

**難易度:** ☆☆☆

## 問題

SSCで、入力を1つ読み、その値を2倍して出力するプログラムを書いてください。

関数 `double_program()` を書き、このプログラムを8ビット命令のリストとして返してください。

## 制約

- 前問までの `assemble_line` と `run` を使って確認してください。
- データはPython整数として扱います。
- `Shift 1` は、Accumulatorの値を1ビット左シフトします。

## 例

```python
>>> run(double_program(), [21])
[42]
>>> run(double_program(), [-3])
[-6]
```

## 発展

`Shift 2` に変えると、どのような計算になるか確認してください。
