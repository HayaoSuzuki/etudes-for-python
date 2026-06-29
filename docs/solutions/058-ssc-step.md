---
title: "058: 「Accumulatorは一つだけ」の解答"
description: "PC、Accumulator、メモリを持つSSCを1命令だけ進める。"
difficulty: 4
---

# 058: 「Accumulatorは一つだけ」の解答

[問題](../problems/058-ssc-step.md) / [ヒント](../hints/058-ssc-step.md)

**難易度:** ☆☆☆☆

## 方針

まず、現在のPCが指す命令を読み、命令名とoperandに分けます。
`next_pc` を `pc + 1` として用意しておき、分岐命令だけ必要に応じて上書きします。
`Jump 0` の場合は `halted` を `True` にします。

## 実装

```python
def make_machine(program=None, inputs=None):
    memory = [0] * 32
    if program is not None:
        for address, value in enumerate(program):
            memory[address] = value
    if inputs is None:
        inputs = []
    return {
        "memory": memory,
        "pc": 0,
        "acc": 0,
        "inputs": list(inputs),
        "outputs": [],
        "halted": False,
    }


def step(machine):
    if machine["halted"]:
        return

    pc = machine["pc"]
    instruction = machine["memory"][pc]
    name, operand = decode_instruction(instruction)
    next_pc = pc + 1

    if name == "Jump":
        if operand == 0:
            machine["halted"] = True
            return
        if machine["acc"] > 0:
            next_pc = operand
    elif name == "Add":
        machine["acc"] += machine["memory"][operand]
    elif name == "Sub":
        machine["acc"] -= machine["memory"][operand]
    elif name == "Load":
        machine["acc"] = machine["memory"][operand]
    elif name == "Store":
        machine["memory"][operand] = machine["acc"]
    elif name == "Read":
        if machine["inputs"] == []:
            raise EOFError("input is empty")
        machine["memory"][operand] = machine["inputs"].pop(0)
    elif name == "Write":
        machine["outputs"].append(machine["memory"][operand])
    elif name == "Shift":
        machine["acc"] <<= operand

    machine["pc"] = next_pc
```

## 確認

```python
machine = make_machine([
    assemble_line("Load 10"),
    assemble_line("Add 11"),
    assemble_line("Store 12"),
    assemble_line("Stop"),
])
machine["memory"][10] = 7
machine["memory"][11] = 5
step(machine)
assert machine["acc"] == 7
step(machine)
assert machine["acc"] == 12
step(machine)
assert machine["memory"][12] == 12
```

## 発展

PCが範囲外のまま `step()` を呼ぶと、Pythonのリストアクセスで `IndexError` が起こります。
エミュレータのエラーとして明示したい場合は、命令を読む前に `0 <= pc < 32` を確認します。
