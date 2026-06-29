---
title: "021: 命令表はコードでもある"
description: "8ビット命令をopcodeとoperandに分け、命令表から相互変換する。"
difficulty: 1
---

# 021: 命令表はコードでもある

[ヒント](../hints/021-ssc-instruction-table.md) / [解答](../solutions/021-ssc-instruction-table.md)

**難易度:** ☆

## 問題

SSCの命令を扱うために、命令表と変換関数を書いてください。

SSC（SlowScanComputer）は、8ビットの命令を使います。
上位3ビットは命令の種類を表す**opcode**です。
下位5ビットは番地またはシフト量を表す**operand**です。

命令は次の8種類です。

| ニーモニック | opcode | operandの意味 |
|---|---:|---|
| `Jump` | `000` | 分岐先の番地 |
| `Add` | `001` | 加算する値の番地 |
| `Sub` | `010` | 減算する値の番地 |
| `Load` | `011` | 読み込む値の番地 |
| `Store` | `100` | 書き込む番地 |
| `Read` | `101` | 入力を書き込む番地 |
| `Write` | `110` | 出力する値の番地 |
| `Shift` | `111` | 左シフトするビット数 |

関数 `decode_instruction(instruction)` と `encode_instruction(name, operand)` を書いてください。

`decode_instruction` は、0以上255以下の整数を受け取り、`(命令名, operand)` のタプルを返します。
`encode_instruction` は、命令名とoperandを受け取り、0以上255以下の整数を返します。

## 制約

- 命令表は辞書 `INSTRUCTIONS` として定義してください。
- `operand` は0以上31以下の整数です。
- 範囲外の命令またはoperandには `ValueError` を送出してください。
- 未知の命令名には `KeyError` を送出してください。

## 例

```python
>>> decode_instruction(0b01100111)
('Load', 7)
>>> encode_instruction("Load", 7)
103
>>> bin(encode_instruction("Shift", 1))
'0b11100001'
>>> decode_instruction(0)
('Jump', 0)
```

## 発展

`Jump 0` は停止命令として扱います。
命令そのものは `Jump` で、operandが0のときだけ停止を意味する点を確認してください。

