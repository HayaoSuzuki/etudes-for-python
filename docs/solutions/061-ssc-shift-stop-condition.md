---
title: "061: 「止まらない二倍の列」の解答"
description: "Python整数版のShiftループと8ビット符号付き解釈の停止条件を比較する。"
difficulty: 4
---

# 061: 「止まらない二倍の列」の解答

[問題](../problems/061-ssc-shift-stop-condition.md) / [ヒント](../hints/061-ssc-shift-stop-condition.md)

**難易度:** ☆☆☆☆

## 方針

Python整数版では、左シフトの結果をそのまま使います。
8ビット符号付き版では、各回の左シフト後に下位8ビットだけを残し、128以上の値を負の値へ変換します。
その値が0以下になったら停止条件に達したとみなします。

## 実装

```python
def to_signed8(value):
    value = value % 256
    if value >= 128:
        return value - 256
    return value


def python_shift_outputs(initial, count):
    value = initial
    outputs = []
    for _ in range(count):
        value = value << 1
        outputs.append(value)
    return outputs


def signed8_shift_until_stop(initial):
    value = initial
    outputs = []
    while True:
        value = to_signed8(value << 1)
        outputs.append(value)
        if value <= 0:
            return outputs
```

## 確認

```python
assert python_shift_outputs(3, 6) == [6, 12, 24, 48, 96, 192]
assert signed8_shift_until_stop(3) == [6, 12, 24, 48, 96, -64]
assert signed8_shift_until_stop(5) == [10, 20, 40, 80, -96]
```

## 発展

Python整数版では、正の値を左シフトし続けても正のままです。
したがって、Accumulatorが正なら分岐する `Jump` だけでは、オーバーフローによる停止は起きません。
`max_steps` のような実行上限を持つ理由がここにあります。
