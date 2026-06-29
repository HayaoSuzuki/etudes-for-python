---
title: "057: ニーモニックの皮をかぶった数"
description: "SSCの1行アセンブリを8ビット命令へ変換する。"
difficulty: 3
---

# 057: ニーモニックの皮をかぶった数

[ヒント](../hints/057-ssc-assembly-line.md) / [解答](../solutions/057-ssc-assembly-line.md)

**難易度:** ☆☆☆

## 問題

関数 `assemble_line(line)` と `disassemble_instruction(instruction)` を書いてください。

`assemble_line` は、`"Load 7"` のような1行のアセンブリ表記を受け取り、8ビット命令を表す整数を返します。
`disassemble_instruction` は、8ビット命令を受け取り、`"Load 7"` のような文字列を返します。

`"Stop"` は、`"Jump 0"` の別名として扱ってください。

## 制約

- 前問の `encode_instruction` と `decode_instruction` を使ってください。
- 命令名とoperandは空白で区切ります。
- 行頭と行末の空白は無視してください。
- `;` 以降はコメントとして無視してください。

## 例

```python
>>> assemble_line("Load 7")
103
>>> assemble_line("  Shift 1  ; double")
225
>>> assemble_line("Stop")
0
>>> disassemble_instruction(103)
'Load 7'
>>> disassemble_instruction(0)
'Stop'
```

## 発展

空行やコメントだけの行を、`None` として扱う版にしてください。
