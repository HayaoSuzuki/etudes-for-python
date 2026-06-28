---
title: "020: 「私の戦闘力は53万」の解答"
description: "正規表現で文字種と危険な形を検出し、点数から強さを分類する。"
---

# 020: 「私の戦闘力は53万」の解答

[問題](../problems/020-password-strength-indicator.md) / [ヒント](../hints/020-password-strength-indicator.md)

## 方針

最初に、使える文字だけで構成されているかを調べます。
使えない文字を含むパスワードは、その時点で `"weak"` とします。

そのあと、長さと文字種で点数を足します。
同じ文字の3連続や、よくある危険な単語を含む場合は点数を引きます。

## 実装

```python
import re


ALLOWED_RE = re.compile(r"[A-Za-z0-9!@#$%^&*]+")
CATEGORY_PATTERNS = (
    re.compile(r"[a-z]"),
    re.compile(r"[A-Z]"),
    re.compile(r"[0-9]"),
    re.compile(r"[!@#$%^&*]"),
)
REPEATED_RE = re.compile(r"(.)\1\1")
COMMON_WORD_RE = re.compile(r"password|qwerty|admin|letmein", re.IGNORECASE)


def password_strength(password: str) -> str:
    if not ALLOWED_RE.fullmatch(password):
        return "weak"

    score = 0

    if len(password) >= 8:
        score += 1
    if len(password) >= 12:
        score += 1
    if len(password) >= 16:
        score += 1

    for pattern in CATEGORY_PATTERNS:
        if pattern.search(password):
            score += 1

    if REPEATED_RE.search(password):
        score -= 1
    if COMMON_WORD_RE.search(password):
        score -= 2

    if score <= 3:
        return "weak"
    if score <= 5:
        return "medium"
    return "strong"
```

## 確認

```python
assert password_strength("password") == "weak"
assert password_strength("Abcdef12") == "medium"
assert password_strength("P@ssw0rd!!!") == "medium"
assert password_strength("R3gex!Vault2026") == "strong"
assert password_strength("R3gex Vault") == "weak"
```

## 考え方

前問では、規則に違反している理由を列挙しました。
この問題では、同じような検査を点数に変換しています。

`COMMON_WORD_RE` では、`re.IGNORECASE` を指定しています。
これにより、`Password` や `PASSWORD` も同じ危険な単語として検出できます。
