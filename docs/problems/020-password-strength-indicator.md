---
title: "020: 私の戦闘力は53万"
description: "正規表現で文字種を数え、パスワードの強さを分類する。"
---

# 020: 私の戦闘力は53万

[ヒント](../hints/020-password-strength-indicator.md) / [解答](../solutions/020-password-strength-indicator.md)

## 問題

関数 `password_strength(password)` を書いてください。
この関数は、パスワードの強さを `"weak"`、`"medium"`、`"strong"` のいずれかで返します。

この問題の指標は、正規表現を練習するための簡略化したものです。
現実のパスワード強度を正確に表すものではありません。

## 採点規則

まず、使える文字だけで構成されているかを確認します。
使える文字は、ASCII英字、数字、記号 `!@#$%^&*` です。
使えない文字を含む場合は、`"weak"` を返してください。

次に、次の条件を満たすたびに点を足します。

- 8文字以上なら1点
- 12文字以上なら1点
- 16文字以上なら1点
- 小文字を含むなら1点
- 大文字を含むなら1点
- 数字を含むなら1点
- 記号 `!@#$%^&*` を含むなら1点

ただし、次の条件に当てはまる場合は点を引きます。

- 同じ文字が3回連続するなら1点引く
- `password`、`qwerty`、`admin`、`letmein` のいずれかを含むなら2点引く

最後に、点数を次のように分類します。

- 3点以下：`"weak"`
- 4点以上5点以下：`"medium"`
- 6点以上：`"strong"`

## 例

```python
>>> password_strength("password")
'weak'
>>> password_strength("Abcdef12")
'medium'
>>> password_strength("P@ssw0rd!!!")
'medium'
>>> password_strength("R3gex!Vault2026")
'strong'
>>> password_strength("R3gex Vault")
'weak'
```
