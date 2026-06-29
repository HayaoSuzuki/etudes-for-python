---
title: "108: メールから件名を取り出す"
description: "emailパッケージでメール文字列を解析し、主要ヘッダーと本文を取り出す。"
difficulty: 4
---

# 108: メールから件名を取り出す

[ヒント](../hints/108-email-header-parser.md) / [解答](../solutions/108-email-header-parser.md)

**難易度:** ☆☆☆☆

## 問題

関数 `parse_email_summary(raw)` を書いてください。

この関数は、メールメッセージ文字列を解析し、件名、差出人、本文を持つ辞書を返します。

## 制約

- `email` パッケージを使ってください。
- `raw` は文字列です。
- 戻り値は、キー `subject`、`from`、`body` を持つ辞書です。
- `Subject` または `From` ヘッダーがない場合は空文字列にしてください。
- 本文は、前後の空白を取り除いて返してください。
- multipartメールの場合は、最初の `text/plain` の本文を返してください。

## 例

```python
>>> raw = "From: alice@example.com\\nSubject: Hello\\n\\nHi there\\n"
>>> parse_email_summary(raw)
{'subject': 'Hello', 'from': 'alice@example.com', 'body': 'Hi there'}
```

## 発展

添付ファイル名の一覧も取り出してください。

## 参考

- [email](https://docs.python.org/ja/3.14/library/email.html)
