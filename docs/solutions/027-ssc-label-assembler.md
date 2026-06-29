---
title: "027: 「ラベルは番地を忘れさせる」の解答"
description: "ラベルとData擬似命令を持つ小さなSSCアセンブラを書く。"
difficulty: 3
---

# 027: 「ラベルは番地を忘れさせる」の解答

[問題](../problems/027-ssc-label-assembler.md) / [ヒント](../hints/027-ssc-label-assembler.md)

**難易度:** ☆☆☆
## 方針

ラベルは、後ろにある番地を前から参照できるようにする仕組みです。
そのため、先にすべてのラベルと番地を集めます。
2回目の走査で、命令やDataを実際の整数に変換します。

## 実装

```python
def clean_line(line):
    return line.split(";", 1)[0].strip()


def split_label(line):
    if ":" not in line:
        return (None, line)
    label, rest = line.split(":", 1)
    return (label.strip(), rest.strip())


def operand_value(text, labels):
    try:
        return int(text)
    except ValueError:
        return labels[text]


def assemble_program(lines):
    labels = {}
    address = 0
    cleaned_lines = []

    for raw_line in lines:
        line = clean_line(raw_line)
        if line == "":
            continue
        label, body = split_label(line)
        if label is not None:
            if label in labels:
                raise ValueError("duplicate label: " + label)
            labels[label] = address
        if body != "":
            cleaned_lines.append(body)
            address += 1

    program = []
    for body in cleaned_lines:
        if body == "Stop":
            program.append(encode_instruction("Jump", 0))
            continue

        parts = body.split()
        if parts[0] == "Data":
            program.append(int(parts[1]))
        else:
            name = parts[0]
            operand = operand_value(parts[1], labels)
            program.append(encode_instruction(name, operand))

    return program
```

## 確認

```python
program = assemble_program([
    "Load value",
    "Shift 1",
    "Store value",
    "Write value",
    "Stop",
    "value: Data 21",
])
assert run(program) == [42]
```

## 発展

ラベル名が未定義の場合は、現在の実装では辞書アクセスによる `KeyError` が起こります。
利用者向けのエラーにしたい場合は、未定義ラベルを明示して `ValueError` を送出します。

