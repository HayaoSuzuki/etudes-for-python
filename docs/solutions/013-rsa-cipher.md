---
title: "013: RSA暗号の解答"
description: "公開鍵と秘密鍵を作り、剰余付きべき乗で暗号化と復号を行う。"
---

# 013: RSA暗号の解答

[問題](../problems/013-rsa-cipher.md) / [ヒント](../hints/013-rsa-cipher.md)

## 方針

RSA暗号では、公開鍵 `(n, e)` と秘密鍵 `(n, d)` を使います。
`d` は、`e` の `phi` における逆元です。

`e` と `phi` が互いに素でなければ、逆元は存在しません。
この判定には、Euclidの互除法による `gcd` を使います。

## 実装

```python
def gcd(a: int, b: int) -> int:
    if a < 0 or b < 0:
        raise ValueError("a and b must be non-negative")
    if a == 0 and b == 0:
        raise ValueError("gcd(0, 0) is undefined")

    while b != 0:
        a, b = b, a % b

    return a


def make_rsa_keys(p: int, q: int, e: int) -> tuple[tuple[int, int], tuple[int, int]]:
    n = p * q
    phi = (p - 1) * (q - 1)

    if gcd(e, phi) != 1:
        raise ValueError("e and phi must be coprime")

    d = pow(e, -1, phi)
    public_key = (n, e)
    private_key = (n, d)
    return public_key, private_key


def rsa_encrypt(message: int, public_key: tuple[int, int]) -> int:
    n, e = public_key

    if not 0 <= message < n:
        raise ValueError("message must satisfy 0 <= message < n")

    return pow(message, e, n)


def rsa_decrypt(ciphertext: int, private_key: tuple[int, int]) -> int:
    n, d = private_key

    if not 0 <= ciphertext < n:
        raise ValueError("ciphertext must satisfy 0 <= ciphertext < n")

    return pow(ciphertext, d, n)
```

## 確認

```python
public_key, private_key = make_rsa_keys(61, 53, 17)

assert gcd(17, 3120) == 1
assert public_key == (3233, 17)
assert private_key == (3233, 2753)
assert rsa_encrypt(65, public_key) == 2790
assert rsa_decrypt(2790, private_key) == 65
assert rsa_decrypt(rsa_encrypt(123, public_key), private_key) == 123
```

## 考え方

`pow(message, e, n)` は、`message ** e % n` と同じ値を返します。
ただし、巨大な整数を途中で作らないため、RSAのような計算に向いています。

この例の `p = 61`、`q = 53`、`e = 17` では、`n = 3233`、`phi = 3120` です。
`gcd(17, 3120)` は1なので、17は3120における逆元を持ちます。
`17 * 2753` を3120で割った余りは1なので、`d = 2753` になります。

## 参考

- [RSA暗号](https://ja.wikipedia.org/wiki/RSA%E6%9A%97%E5%8F%B7)
