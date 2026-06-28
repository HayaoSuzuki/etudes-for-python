---
title: "021: 世界の合言葉は森"
description: "secretsで候補を作り、正規表現で条件を満たすまで生成する。"
---

# 021: 世界の合言葉は森

[ヒント](../hints/021-password-generator.md) / [解答](../solutions/021-password-generator.md)

## 問題

関数 `generate_password(length=16)` を書いてください。
この関数は、指定された長さのパスワードを生成して返します。

生成するパスワードは、次の条件を満たす必要があります。

- 長さは `length` である
- ASCII英字、数字、記号 `!@#$%^&*` だけを使う
- 小文字を1文字以上含む
- 大文字を1文字以上含む
- 数字を1文字以上含む
- 記号 `!@#$%^&*` を1文字以上含む
- 同じ文字が3回連続しない

乱数には、`random` ではなく `secrets` を使ってください。
`length` が8未満の場合は、`ValueError` を送出してください。

## 例

```python
>>> password = generate_password()
>>> len(password)
16
>>> is_valid_generated_password(password)
True
>>> password = generate_password(24)
>>> len(password)
24
>>> is_valid_generated_password(password)
True
```
