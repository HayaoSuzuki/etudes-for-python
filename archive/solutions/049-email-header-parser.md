---
title: "049: 「メールから件名を取り出す」の解答"
description: "email.parserでメール文字列を解析し、ヘッダーとplain text本文を取り出す。"
difficulty: 4
---

# 049: 「メールから件名を取り出す」の解答

[問題](../problems/049-email-header-parser.md) / [ヒント](../hints/049-email-header-parser.md)

**難易度:** ☆☆☆☆

## 方針

`Parser(policy=policy.default)` で文字列を解析します。
ヘッダーは辞書のように読み、本文は `get_body` または `get_content` で取り出します。

multipartでは、最初の `text/plain` の本文を使います。

## 実装

```python
from email import policy
from email.parser import Parser


def parse_email_summary(raw):
    message = Parser(policy=policy.default).parsestr(raw)

    body_part = message.get_body(preferencelist=("plain",))
    if body_part is None:
        body = message.get_content()
    else:
        body = body_part.get_content()

    return {
        "subject": str(message["Subject"] or ""),
        "from": str(message["From"] or ""),
        "body": body.strip(),
    }
```

## 確認

```python
raw = "From: alice@example.com\nSubject: Hello\n\nHi there\n"

assert parse_email_summary(raw) == {
    "subject": "Hello",
    "from": "alice@example.com",
    "body": "Hi there",
}
```

## 発展

メールには文字コード、添付ファイル、HTML本文など多くの要素があります。
本文を1つの文字列として扱うだけでよいのか、用途に応じて仕様を分けます。

## 参考

- [email](https://docs.python.org/ja/3.14/library/email.html)

