---
title: "015: 「宇宙の鍵は3,6,9」の解答"
description: "包含関係のある倍数条件を優先順位つきの分岐で扱う。"
difficulty: 2
---

# 015: 「宇宙の鍵は3,6,9」の解答

[問題](../problems/015-alternative-fuzzbuzz.md) / [ヒント](../hints/015-alternative-fuzzbuzz.md)

**難易度:** ☆☆

## 方針

6の倍数は3の倍数でもあります。
9の倍数も3の倍数です。
18は、3、6、9のすべての倍数です。

この問題では、当てはまる文字列を連結しません。
上に書いた規則を優先するため、9、6、3の順に条件を調べます。

## 実装

```python
def alternative_fuzzbuzz(n: int) -> list[str]:
    result = []

    for i in range(1, n + 1):
        if i % 9 == 0:
            result.append("Buzz")
        elif i % 6 == 0:
            result.append("Fuzz")
        elif i % 3 == 0:
            result.append("Fizz")
        else:
            result.append(str(i))

    return result
```

## 確認

```python
assert alternative_fuzzbuzz(9) == [
    "1",
    "2",
    "Fizz",
    "4",
    "5",
    "Fuzz",
    "7",
    "8",
    "Buzz",
]
assert alternative_fuzzbuzz(18)[-1] == "Buzz"
```

## 発展

3の倍数判定を最初に書くと、6や9の倍数もそこで止まります。
条件に包含関係がある場合は、より狭い条件から先に調べると、優先順位をコードに反映できます。

