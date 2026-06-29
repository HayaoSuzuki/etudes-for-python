---
title: "010: 檸檬"
description: "繰り返す鍵を使って英大文字を暗号化する。"
difficulty: 3
---

# 010: 檸檬

[ヒント](../hints/010-vigenere-cipher.md) / [解答](../solutions/010-vigenere-cipher.md)

**難易度:** ☆☆☆

## 問題

関数 `vigenere_encrypt(text, key)` と `vigenere_decrypt(text, key)` を書いてください。
この2つの関数は、英大文字だけを対象にしてヴィジュネル暗号の暗号化と復号を行います。

鍵の各文字は、ずらす量を表します。
`A` は0、`B` は1、`C` は2として扱い、`Z` は25として扱います。

平文または暗号文が鍵より長い場合は、鍵を先頭から繰り返して使ってください。
空白や記号は変換せず、鍵も進めません。

## 制約

- `text` は文字列です。
- `key` は空でない文字列です。
- `key` は `A` から `Z` までの英大文字だけで構成されます。
- 変換対象は `A` から `Z` までの英大文字だけです。
- 変換対象外の文字は、そのまま残します。

## 例

```python
>>> vigenere_encrypt("ATTACKATDAWN", "LEMON")
'LXFOPVEFRNHR'
>>> vigenere_decrypt("LXFOPVEFRNHR", "LEMON")
'ATTACKATDAWN'
>>> vigenere_encrypt("ATTACK AT DAWN", "LEMON")
'LXFOPV EF RNHR'
>>> vigenere_encrypt("A-A", "BC")
'B-C'

```
