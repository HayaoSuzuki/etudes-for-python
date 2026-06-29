---
title: "009: 小さな鍵、大きな秘密"
description: "小さい素数を使ってRSA暗号の鍵生成と暗号化を実装する。"
difficulty: 2
---

# 009: 小さな鍵、大きな秘密

[ヒント](../hints/009-rsa-cipher.md) / [解答](../solutions/009-rsa-cipher.md)

**難易度:** ☆☆

## 問題

関数 `make_rsa_keys(p, q, e)`、`rsa_encrypt(message, public_key)`、`rsa_decrypt(ciphertext, private_key)` を書いてください。
この問題では、小さい素数を使ってRSA暗号の鍵生成、暗号化、復号を扱います。

`make_rsa_keys` は、2つの素数 `p` と `q` と公開指数 `e` から、公開鍵と秘密鍵を作って返します。
`rsa_encrypt` は公開鍵で `message` を暗号化し、`rsa_decrypt` は秘密鍵で `ciphertext` を復号します。
公開鍵は `(n, e)`、秘密鍵は `(n, d)` の形とします。
`n` は2つの素数の積 `p * q` です。

この問題の数は学習用です。
実用の暗号には使えません。

## 制約

- `p` と `q` は異なる素数です。
- `e` は公開指数で、秘密指数 `d` が定まるように選ばれます。
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

