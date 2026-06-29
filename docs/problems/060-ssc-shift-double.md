---
title: "060: 左に寄せれば二倍になる"
description: "Shift命令を使って入力値を2倍し、SSCで出力する。"
difficulty: 3
---

# 060: 左に寄せれば二倍になる

[ヒント](../hints/060-ssc-shift-double.md) / [解答](../solutions/060-ssc-shift-double.md)

**難易度:** ☆☆☆

## 問題

SSCで、入力値を2倍して出力するプログラムを書いてください。

プログラムは、次の動きをします。

1. 入力装置から値を読み、31番地に保存する。
2. 31番地の値をAccumulatorへ読み込む。
3. Accumulatorを1ビット左シフトする。
4. 結果を31番地へ保存する。
5. 31番地の値を出力する。
6. 停止する。

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
