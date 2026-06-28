---
title: "013: 小さな鍵、大きな秘密"
description: "小さい素数を使ってRSA暗号の鍵生成と暗号化を実装する。"
---

# 013: 小さな鍵、大きな秘密

[ヒント](../hints/013-rsa-cipher.md) / [解答](../solutions/013-rsa-cipher.md)

## 問題

関数 `make_rsa_keys(p, q, e)`、`rsa_encrypt(message, public_key)`、`rsa_decrypt(ciphertext, private_key)` を書いてください。
この問題では、小さい素数を使ってRSA暗号の鍵生成、暗号化、復号を扱います。

2つの素数 `p` と `q` から、`n = p * q` を作ります。
`phi = (p - 1) * (q - 1)` とし、`(e * d) % phi == 1` を満たす `d` を求めます。

公開鍵は `(n, e)`、秘密鍵は `(n, d)` とします。
暗号化は `pow(message, e, n)`、復号は `pow(ciphertext, d, n)` で行います。

`p` と `q` が素数であることは、前問の `primes_up_to` で確認できます。
`e` と `phi` が互いに素かどうかは、`gcd` で判定してください。
この問題の数は学習用です。
実用の暗号には使えません。

## 制約

- `p` と `q` は異なる素数です。
- `e` は `phi` と互いに素な整数です。
- `message` は `0 <= message < n` を満たす整数です。
- `ciphertext` は `0 <= ciphertext < n` を満たす整数です。
- 文字列の変換は扱わず、整数だけを暗号化します。

## 例

```python
>>> public_key, private_key = make_rsa_keys(61, 53, 17)
>>> public_key
(3233, 17)
>>> private_key
(3233, 2753)
>>> rsa_encrypt(65, public_key)
2790
>>> rsa_decrypt(2790, private_key)
65

```

## 確認

別の小さい整数でも、暗号化してから復号すると元に戻ることを確かめてください。

```python
>>> public_key, private_key = make_rsa_keys(61, 53, 17)
>>> rsa_decrypt(rsa_encrypt(123, public_key), private_key)
123

```
