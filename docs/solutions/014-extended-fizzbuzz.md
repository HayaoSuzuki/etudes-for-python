---
title: "014: 「七五三」の解答"
description: "独立したif文で複数の倍数条件を組み合わせる。"
difficulty: 2
---

# 014: 「七五三」の解答

[問題](../problems/014-extended-fizzbuzz.md) / [ヒント](../hints/014-extended-fizzbuzz.md)

**難易度:** ☆☆

## 方針

1から `n` までを `for` 文で順に調べます。
各数について、出力する文字列をいったん空にします。

3、5、7の倍数判定は独立した条件です。
15のように複数の条件を満たす数があるため、`elif` で分岐を打ち切らず、`if` を並べます。

## 実装

```python
def extended_fizzbuzz(n: int) -> list[str]:
    result = []

    for i in range(1, n + 1):
        word = ""

        if i % 3 == 0:
            word += "Fizz"
        if i % 5 == 0:
            word += "Buzz"
        if i % 7 == 0:
            word += "Bazz"

        if word == "":
            word = str(i)

        result.append(word)

    return result
```

## 確認

```python
assert extended_fizzbuzz(7) == [
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "Bazz",
]
assert extended_fizzbuzz(15)[-1] == "FizzBuzz"
assert extended_fizzbuzz(21)[-1] == "FizzBazz"
assert extended_fizzbuzz(35)[-1] == "BuzzBazz"
assert extended_fizzbuzz(105)[-1] == "FizzBuzzBazz"
```

## 発展

`elif` を使うと、最初に当たった条件だけが実行されます。
その場合、15、21、35、105のような数で必要な文字列を作れません。

