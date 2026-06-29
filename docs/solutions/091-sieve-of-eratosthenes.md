---
title: "091: 「夜の金網をくぐり抜け」の解答"
description: "素数候補のリストから倍数を消して素数を残す。"
difficulty: 3
---

# 091: 「夜の金網をくぐり抜け」の解答

[問題](../problems/091-sieve-of-eratosthenes.md) / [ヒント](../hints/091-sieve-of-eratosthenes.md)

**難易度:** ☆☆☆

## 方針

0から `n` までの整数について、素数候補かどうかをリストで持ちます。
最初に0と1を素数ではないものとして消します。

次に、2から順に候補を見ます。
候補として残っている数 `p` があれば、`p * p` から始めて `p` の倍数を消します。

## 実装

```python
def primes_up_to(n: int) -> list[int]:
    if n < 0:
        raise ValueError("n must be non-negative")

    is_prime = [True] * (n + 1)

    is_prime[0] = False
    if n >= 1:
        is_prime[1] = False

    p = 2
    while p * p <= n:
        if is_prime[p]:
            for multiple in range(p * p, n + 1, p):
                is_prime[multiple] = False
        p += 1

    return [number for number, prime in enumerate(is_prime) if prime]
```

## 確認

```python
assert primes_up_to(0) == []
assert primes_up_to(1) == []
assert primes_up_to(2) == [2]
assert primes_up_to(30) == [2, 3, 5, 7, 11, 13, 17, 19, 23, 29]
assert primes_up_to(100)[-2:] == [89, 97]

primes = primes_up_to(100)
assert 53 in primes
assert 61 in primes
```

## 考え方

`p` が素数なら、`p` の倍数は `p` で割り切れるので素数ではありません。
この操作を小さい素数から順に行うと、合成数だけが消え、素数が候補として残ります。

`p * p` より小さい `p` の倍数は、すでにより小さい約数を持っています。
そのため、倍数を消す処理は `p * p` から始められます。

## 参考

- [エラトステネスの篩](https://ja.wikipedia.org/wiki/%E3%82%A8%E3%83%A9%E3%83%88%E3%82%B9%E3%83%86%E3%83%8D%E3%82%B9%E3%81%AE%E7%AF%A9)

