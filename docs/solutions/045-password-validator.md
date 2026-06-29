---
title: "045: 「紅美鈴はよく眠る」の解答"
description: "fullmatchとsearchを使い分けて、パスワード規則を検査する。"
difficulty: 3
---

# 045: 「紅美鈴はよく眠る」の解答

[問題](../problems/045-password-validator.md) / [ヒント](../hints/045-password-validator.md)

**難易度:** ☆☆☆

## 方針

長さは `len` で調べます。
文字の集合や、特定の種類の文字を含むかどうかは正規表現で調べます。

使える文字だけで構成されているかは `fullmatch` で調べます。
小文字、大文字、数字、記号を含むかどうかは `search` で調べます。

## 実装

```python
import re


ALLOWED_RE = re.compile(r"[A-Za-z0-9!@#$%^&*]+")
LOWERCASE_RE = re.compile(r"[a-z]")
UPPERCASE_RE = re.compile(r"[A-Z]")
DIGIT_RE = re.compile(r"[0-9]")
SYMBOL_RE = re.compile(r"[!@#$%^&*]")
REPEATED_RE = re.compile(r"(.)\1\1")


def validate_password(password: str) -> list[str]:
    errors = []

    if len(password) < 8:
        errors.append("too_short")
    if len(password) > 20:
        errors.append("too_long")
    if not ALLOWED_RE.fullmatch(password):
        errors.append("invalid_character")
    if not LOWERCASE_RE.search(password):
        errors.append("missing_lowercase")
    if not UPPERCASE_RE.search(password):
        errors.append("missing_uppercase")
    if not DIGIT_RE.search(password):
        errors.append("missing_digit")
    if not SYMBOL_RE.search(password):
        errors.append("missing_symbol")
    if REPEATED_RE.search(password):
        errors.append("repeated_character")

    return errors


def is_valid_password(password: str) -> bool:
    return validate_password(password) == []
```

## 確認

```python
assert validate_password("Abcdef1!") == []
assert validate_password("abcdef1!") == ["missing_uppercase"]
assert validate_password("ABCDEF1!") == ["missing_lowercase"]
assert validate_password("Abcdef!!") == ["missing_digit"]
assert validate_password("Abc111!!") == ["repeated_character"]
assert validate_password("Abc def1!") == ["invalid_character"]
assert is_valid_password("Abcdef1!")
assert not is_valid_password("password")
```

## 考え方

`fullmatch` は、文字列全体が正規表現に一致するかを調べます。
この問題では、使える文字だけで構成されているかを確認するために使っています。

`search` は、文字列のどこかに一致する部分があるかを調べます。
小文字を含むか、数字を含むか、といった検査には `search` が向いています。
