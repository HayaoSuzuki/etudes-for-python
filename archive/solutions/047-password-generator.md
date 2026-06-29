---
title: "047: 「世界の合言葉は森」の解答"
description: "secretsで候補を作り、正規表現で条件を満たすまで生成する。"
difficulty: 4
---

# 047: 「世界の合言葉は森」の解答

[問題](../problems/047-password-generator.md) / [ヒント](../hints/047-password-generator.md)

**難易度:** ☆☆☆☆

## 方針

`secrets.choice` を使って、使える文字集合から1文字ずつ選びます。
できた候補が条件を満たすかどうかは、正規表現で検査します。

候補が条件を満たさない場合は、もう一度生成します。
この方法なら、生成処理と検査処理を分けて書けます。

## 実装

```python
import re
import secrets
import string


SYMBOLS = "!@#$%^&*"
ALPHABET = string.ascii_letters + string.digits + SYMBOLS
ALLOWED_RE = re.compile(r"[A-Za-z0-9!@#$%^&*]+")
LOWERCASE_RE = re.compile(r"[a-z]")
UPPERCASE_RE = re.compile(r"[A-Z]")
DIGIT_RE = re.compile(r"[0-9]")
SYMBOL_RE = re.compile(r"[!@#$%^&*]")
REPEATED_RE = re.compile(r"(.)\1\1")


def is_valid_generated_password(password: str) -> bool:
    return bool(
        ALLOWED_RE.fullmatch(password)
        and LOWERCASE_RE.search(password)
        and UPPERCASE_RE.search(password)
        and DIGIT_RE.search(password)
        and SYMBOL_RE.search(password)
        and not REPEATED_RE.search(password)
    )


def generate_password(length: int = 16) -> str:
    if length < 8:
        raise ValueError("length must be at least 8")

    while True:
        password = "".join(secrets.choice(ALPHABET) for _ in range(length))
        if is_valid_generated_password(password):
            return password
```

## 確認

```python
for length in (8, 16, 24):
    password = generate_password(length)
    assert len(password) == length
    assert is_valid_generated_password(password)

try:
    generate_password(7)
except ValueError:
    pass
else:
    raise AssertionError("generate_password(7) must raise ValueError")
```

## 考え方

`secrets` は、パスワードやトークンのような用途の乱数を扱うためのモジュールです。
この問題では、候補の1文字を選ぶために `secrets.choice` を使います。

生成器の中にすべての条件を埋め込むと、処理が読みにくくなります。
先に検査関数を作り、生成器は候補を作って検査するだけにすると、正規表現の役割がはっきりします。

