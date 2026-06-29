---
title: "021: 「命令表はコードでもある」の解答"
description: "8ビット命令をopcodeとoperandに分け、命令表から相互変換する。"
difficulty: 1
---

# 021: 「命令表はコードでもある」の解答

[問題](../problems/021-ssc-instruction-table.md) / [ヒント](../hints/021-ssc-instruction-table.md)

**難易度:** ☆

## 方針

命令表を1つ定義し、そこから逆引き用の辞書を作ります。
デコードでは、命令を `>> 5` で右にずらしてopcodeを取り出します。
operandは下位5ビットなので、`& 0b11111` で取り出せます。

## 実装

```python
INSTRUCTIONS = {
    "Jump": {"opcode": 0b000, "operand": "address"},
    "Add": {"opcode": 0b001, "operand": "address"},
    "Sub": {"opcode": 0b010, "operand": "address"},
    "Load": {"opcode": 0b011, "operand": "address"},
    "Store": {"opcode": 0b100, "operand": "address"},
    "Read": {"opcode": 0b101, "operand": "address"},
    "Write": {"opcode": 0b110, "operand": "address"},
    "Shift": {"opcode": 0b111, "operand": "bits"},
}

OPCODE_TO_NAME = {}
for name, spec in INSTRUCTIONS.items():
    OPCODE_TO_NAME[spec["opcode"]] = name


def decode_instruction(instruction):
    if instruction < 0 or instruction > 255:
        raise ValueError("instruction must be an 8-bit integer")
    opcode = instruction >> 5
    operand = instruction & 0b11111
    return (OPCODE_TO_NAME[opcode], operand)


def encode_instruction(name, operand):
    if operand < 0 or operand > 31:
        raise ValueError("operand must be between 0 and 31")
    opcode = INSTRUCTIONS[name]["opcode"]
    return (opcode << 5) | operand
```

## 確認

```python
assert decode_instruction(0b01100111) == ("Load", 7)
assert encode_instruction("Load", 7) == 103
assert bin(encode_instruction("Shift", 1)) == "0b11100001"
assert decode_instruction(0) == ("Jump", 0)
```

## 発展

`Jump 0` は `opcode=000`、`operand=00000` の命令です。
命令の値としては0なので、メモリを0で初期化すると未使用領域は停止命令になります。

