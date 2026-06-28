---
title: "019: 紅美鈴はよく眠る"
description: "正規表現を使って、パスワードが規則を満たすか検査する。"
---

# 019: 紅美鈴はよく眠る

[ヒント](../hints/019-password-validator.md) / [解答](../solutions/019-password-validator.md)

## 問題

関数 `validate_password(password)` を書いてください。
この関数は、パスワードが規則を満たさない理由をリストで返します。
すべての規則を満たす場合は、空のリストを返します。

この問題の規則は、正規表現を練習するためのものです。
現実のサービスで使うパスワード規則そのものではありません。

## 規則

パスワードは、次の条件を満たす必要があります。

- 8文字以上である
- 20文字以下である
- ASCII英字、数字、記号 `!@#$%^&*` だけを使う
- 小文字を1文字以上含む
- 大文字を1文字以上含む
- 数字を1文字以上含む
- 記号 `!@#$%^&*` を1文字以上含む
- 同じ文字が3回連続しない

## 戻り値

違反した規則に対応する文字列を、次の順番で返してください。

- `too_short`
- `too_long`
- `invalid_character`
- `missing_lowercase`
- `missing_uppercase`
- `missing_digit`
- `missing_symbol`
- `repeated_character`

## 例

```python
>>> validate_password("Abcdef1!")
[]
>>> validate_password("abcdef1!")
['missing_uppercase']
>>> validate_password("ABCDEF1!")
['missing_lowercase']
>>> validate_password("Abcdef!!")
['missing_digit']
>>> validate_password("Abc111!!")
['repeated_character']
>>> validate_password("Abc def1!")
['invalid_character']
```
