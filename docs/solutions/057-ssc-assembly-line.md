---
title: "057: 「ニーモニックの皮をかぶった数」の解答"
description: "SSCの1行アセンブリを8ビット命令へ変換する。"
difficulty: 3
---

# 057: 「ニーモニックの皮をかぶった数」の解答

[問題](../problems/057-ssc-assembly-line.md) / [ヒント](../hints/057-ssc-assembly-line.md)

**難易度:** ☆☆☆

## 方針

アセンブリ表記を、命令名とoperandに分けます。
コメントは先に取り除きます。
`Stop` だけはoperandを持たない別名として扱います。

## 実装

```python
def assemble_line(line):
    line = line.split(";", 1)[0].strip()
    if line == "Stop":
        return encode_instruction("Jump", 0)

    name, operand_text = line.split()
    return encode_instruction(name, int(operand_text))


def disassemble_instruction(instruction):
    name, operand = decode_instruction(instruction)
    if name == "Jump" and operand == 0:
        return "Stop"
    return name + " " + str(operand)
```

## 確認

```python
assert assemble_line("Load 7") == 103
assert assemble_line("  Shift 1  ; double") == 225
assert assemble_line("Stop") == 0
assert disassemble_instruction(103) == "Load 7"
assert disassemble_instruction(0) == "Stop"
```

## 発展

空行やコメントだけの行を許す場合は、コメント除去後の文字列が空かどうかを調べます。
空なら命令を生成せず、`None` を返します。
