---
title: "042: ASCIIは二度回る"
description: "印字可能ASCII文字を任意の数だけ回転する。"
difficulty: 3
---

# 042: ASCIIは二度回る

[ヒント](../hints/042-rotate-printable-ascii.md) / [解答](../solutions/042-rotate-printable-ascii.md)

**難易度:** ☆☆☆

## 問題

関数 `rotate_printable_ascii(text, shift)` を書いてください。
この関数は、文字列 `text` に含まれる `!` から `~` までのASCII文字を、`shift` 文字ぶん右へ回転します。

この問題では、空白は回転対象に含めません。
`!` より前、または `~` より後の文字は、そのまま残してください。

## 制約

- `text` は文字列です。
- `shift` は整数です。
- `shift` は0、正の数、負の数のいずれも取りえます。
- 回転対象はASCIIコード33から126までの94文字です。
- 対象外の文字は変更しません。

## 例

```python
>>> rotate_printable_ascii("Hello", 47)
'w6==@'
>>> rotate_printable_ascii("w6==@", 47)
'Hello'
>>> rotate_printable_ascii("!", -1)
'~'
>>> rotate_printable_ascii("Hello, World!", 94)
'Hello, World!'

```

## 確認

前問の暗号文は、`shift` に47を指定すると復号できます。

```python
>>> rotate_printable_ascii("$FA6C42=:7C28:=:DE:46IA:2=:5@4:@FD", 47)
'Supercalifragilisticexpialidocious'

```
