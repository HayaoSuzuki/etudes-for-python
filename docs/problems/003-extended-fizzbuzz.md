---
title: "003: 七五三"
description: "3、5、7の倍数に応じて文字列を作る関数を書く。"
---

# 003: 七五三

[ヒント](../hints/003-extended-fizzbuzz.md) / [解答](../solutions/003-extended-fizzbuzz.md)

## 問題

整数 `n` を受け取り、1から `n` までの各整数を次の規則で文字列に変換する関数 `extended_fizzbuzz` を書いてください。

- 3の倍数なら `Fizz` を含めます。
- 5の倍数なら `Buzz` を含めます。
- 7の倍数なら `Bazz` を含めます。
- 複数の条件を満たす場合は、`Fizz`、`Buzz`、`Bazz` の順につなげます。
- どの条件も満たさない場合は、数値を文字列にします。

関数は、変換した文字列を順番に並べたリストを返します。

## 制約

- `n` は1以上の整数です。

## 例

```python
>>> extended_fizzbuzz(7) == [
...     "1",
...     "2",
...     "Fizz",
...     "4",
...     "Buzz",
...     "Fizz",
...     "Bazz",
... ]
True
>>> extended_fizzbuzz(15)[-1]
'FizzBuzz'
>>> extended_fizzbuzz(21)[-1]
'FizzBazz'

```

## 発展

105を渡したとき、最後の要素がどうなるかを確認してください。
