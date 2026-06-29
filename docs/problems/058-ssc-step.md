---
title: "058: Accumulatorは一つだけ"
description: "PC、Accumulator、メモリを持つSSCを1命令だけ進める。"
difficulty: 4
---

# 058: Accumulatorは一つだけ

[ヒント](../hints/058-ssc-step.md) / [解答](../solutions/058-ssc-step.md)

**難易度:** ☆☆☆☆

## 問題

SSCの状態を作る関数 `make_machine(program=None, inputs=None)` と、状態を1命令だけ進める関数 `step(machine)` を書いてください。

`machine` は次のキーを持つ辞書です。

- `"memory"`：長さ32のリスト
- `"pc"`：次に実行する番地
- `"acc"`：Accumulatorの値
- `"inputs"`：入力値のリスト
- `"outputs"`：出力値のリスト
- `"halted"`：停止しているかどうか

`make_machine` は、`program` をメモリの先頭から順に置き、残りを0で埋めた初期状態の辞書を返します。
`inputs` は `Read` 命令が読む入力値のリストで、`pc` と `acc` は0、`outputs` は空、`halted` は偽から始めます。
`step` は、現在の `pc` が指すメモリから命令を読みます。
データはPython整数として扱い、8ビットに丸めません。

## 制約

- 前問までの `decode_instruction` を使ってください。
- `Jump 0` は停止命令です。
- `Jump n` は、Accumulatorが正のときだけ `n` 番地へ分岐します。
- 分岐しない命令では、`pc` を1増やします。
- `Read` で入力が空の場合は `EOFError` を送出してください。

## 例

```python
>>> machine = make_machine([assemble_line("Load 10"), assemble_line("Add 11"), assemble_line("Store 12"), assemble_line("Stop")])
>>> machine["memory"][10] = 7
>>> machine["memory"][11] = 5
>>> step(machine)
>>> machine["acc"]
7
>>> step(machine)
>>> machine["acc"]
12
>>> step(machine)
>>> machine["memory"][12]
12
```

## 発展

`pc` が0以上31以下でない場合のエラー処理を追加してください。
