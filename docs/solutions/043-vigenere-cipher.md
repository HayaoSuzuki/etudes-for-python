---
title: "043: 「檸檬」の解答"
description: "鍵を繰り返しながら英大文字を26文字の範囲で回転する。"
difficulty: 3
---

# 043: 「檸檬」の解答

[問題](../problems/043-vigenere-cipher.md) / [ヒント](../hints/043-vigenere-cipher.md)

**難易度:** ☆☆☆

## 方針

英大文字を `A` から始まる0から25までの番号として扱います。
鍵の文字も同じ番号に変換し、その値をシフト量にします。

空白や記号では鍵を進めません。
そのため、`text` の添字とは別に、変換した英大文字の数を数えます。

## 実装

```python
def rotate_upper(char: str, shift: int) -> str:
    start = ord("A")
    size = 26
    return chr(start + ((ord(char) - start + shift) % size))


def vigenere_encrypt(text: str, key: str) -> str:
    if not key:
        raise ValueError("key must not be empty")

    result = []
    key_index = 0

    for char in text:
        if "A" <= char <= "Z":
            key_char = key[key_index % len(key)]
            shift = ord(key_char) - ord("A")
            result.append(rotate_upper(char, shift))
            key_index += 1
        else:
            result.append(char)

    return "".join(result)


def vigenere_decrypt(text: str, key: str) -> str:
    if not key:
        raise ValueError("key must not be empty")

    result = []
    key_index = 0

    for char in text:
        if "A" <= char <= "Z":
            key_char = key[key_index % len(key)]
            shift = ord(key_char) - ord("A")
            result.append(rotate_upper(char, -shift))
            key_index += 1
        else:
            result.append(char)

    return "".join(result)
```

## 確認

```python
assert vigenere_encrypt("ATTACKATDAWN", "LEMON") == "LXFOPVEFRNHR"
assert vigenere_decrypt("LXFOPVEFRNHR", "LEMON") == "ATTACKATDAWN"
assert vigenere_encrypt("ATTACK AT DAWN", "LEMON") == "LXFOPV EF RNHR"
assert vigenere_decrypt("LXFOPV EF RNHR", "LEMON") == "ATTACK AT DAWN"
assert vigenere_encrypt("A-A", "BC") == "B-C"
assert vigenere_decrypt("B-C", "BC") == "A-A"
```

## 考え方

`key_index` は、変換対象の英大文字を処理したときだけ増やします。
この規則にすると、空白や記号の有無に左右されず、文字だけに鍵が対応します。

暗号化と復号の違いは、シフト量の符号だけです。
共通の `rotate_upper` を使うと、26で割った余りの処理を一箇所にまとめられます。

## 参考

- [ヴィジュネル暗号](https://ja.wikipedia.org/wiki/%E3%83%B4%E3%82%A3%E3%82%B8%E3%83%A5%E3%83%8D%E3%83%AB%E6%9A%97%E5%8F%B7)

