---
title: "024: 「Jump 0で眠る機械」の解答"
description: "SSCプログラムを停止命令まで実行し、出力を返す。"
difficulty: 2
---

# 024: 「Jump 0で眠る機械」の解答

[問題](../problems/024-ssc-run.md) / [ヒント](../hints/024-ssc-run.md)

**難易度:** ☆☆

## 方針

`make_machine` で状態を作り、停止するまで `step()` を呼びます。
停止しないプログラムもあり得るので、実行命令数が `max_steps` に達したら例外を送出します。

## 実装

```python
def run(program, inputs=None, max_steps=1000):
    machine = make_machine(program, inputs)
    steps = 0
    while not machine["halted"]:
        if steps >= max_steps:
            raise RuntimeError("program did not halt")
        step(machine)
        steps += 1
    return machine["outputs"]
```

## 確認

```python
program = [
    assemble_line("Read 10"),
    assemble_line("Write 10"),
    assemble_line("Stop"),
]
assert run(program, [42]) == [42]
assert run([assemble_line("Stop")]) == []
```

## 発展

エミュレータをデバッグするときは、停止時の出力だけでは足りません。
`run_machine()` のような別関数を作り、停止時の `machine` を返すと、メモリやAccumulatorを確認できます。

