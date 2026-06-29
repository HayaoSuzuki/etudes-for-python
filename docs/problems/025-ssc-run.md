---
title: "025: Jump 0で眠る機械"
description: "SSCプログラムを停止命令まで実行し、出力を返す。"
difficulty: 2
---

# 025: Jump 0で眠る機械

[ヒント](../hints/025-ssc-run.md) / [解答](../solutions/025-ssc-run.md)

**難易度:** ☆☆
## 問題

関数 `run(program, inputs=None, max_steps=1000)` を書いてください。
この関数は、SSCプログラムを `Jump 0` で停止するまで実行し、出力値のリストを返します。

`program` は、メモリ0番地から順に配置する整数のリストです。
不足するメモリは0で埋めます。
`inputs` は `Read` 命令が読む値のリストです。

## 制約

- 前問の `make_machine` と `step` を使ってください。
- `max_steps` 回実行しても停止しない場合は `RuntimeError` を送出してください。
- 返り値は `machine["outputs"]` です。

## 例

```python
>>> program = [
...     assemble_line("Read 10"),
...     assemble_line("Write 10"),
...     assemble_line("Stop"),
... ]
>>> run(program, [42])
[42]
>>> run([assemble_line("Stop")])
[]
```

## 発展

停止時のメモリやAccumulatorも観察できるように、出力だけでなく `machine` 全体を返す関数を書いてください。

