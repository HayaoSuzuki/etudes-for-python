---
title: "027: ラベルは番地を忘れさせる"
description: "ラベルとData擬似命令を持つ小さなSSCアセンブラを書く。"
difficulty: 3
---

# 027: ラベルは番地を忘れさせる

[ヒント](../hints/027-ssc-label-assembler.md) / [解答](../solutions/027-ssc-label-assembler.md)

**難易度:** ☆☆☆

## 問題

ラベル付きのSSCアセンブラ `assemble_program(lines)` を書いてください。

入力は、アセンブリの各行を文字列として並べたリストです。
行には、次の要素を含められます。

- `label:`：その行の番地に名前を付ける。
- `Load label` のような命令：operandにラベル名を書ける。
- `Data value`：命令ではなく、Python整数のデータをその番地に置く。
- `Stop`：`Jump 0` の別名。
- `;` 以降のコメント。

返り値は、メモリ0番地から順に配置する整数のリストです。

## 制約

- ラベルは、定義より前の行からでも参照できます。
- `Data` の値は8ビットに丸めません。
- 命令は前問までの `encode_instruction` を使って8ビット整数にしてください。
- 空行とコメントだけの行は無視してください。

## 例

```python
>>> program = assemble_program([
...     "Load value",
...     "Shift 1",
...     "Store value",
...     "Write value",
...     "Stop",
...     "value: Data 21",
... ])
>>> run(program)
[42]
```

## 発展

同じラベルが2回定義された場合に `ValueError` を送出してください。

