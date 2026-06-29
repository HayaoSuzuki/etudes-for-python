---
title: "072: 「URLはクエリを背負って走る」の解答"
description: "urllib.parseでURLとクエリ文字列を組み立てる。"
difficulty: 2
---

# 072: 「URLはクエリを背負って走る」の解答

[問題](../problems/072-url-query-builder.md) / [ヒント](../hints/072-url-query-builder.md)

**難易度:** ☆☆

## 方針

まず `urljoin` でURLの本体を作ります。
パラメータがある場合だけ `urlencode` でクエリ文字列を作り、`?` でつなぎます。

## 実装

```python
from urllib.parse import urlencode, urljoin


def build_url(base, path, params):
    url = urljoin(base, path)
    if not params:
        return url
    return f"{url}?{urlencode(params, doseq=True)}"
```

## 確認

```python
assert build_url(
    "https://api.example.com/v1/",
    "search",
    {"q": "猫 Python", "tag": ["howto", "stdlib"]},
) == "https://api.example.com/v1/search?q=%E7%8C%AB+Python&tag=howto&tag=stdlib"

assert build_url(
    "https://api.example.com/v1/",
    "users/42",
    {},
) == "https://api.example.com/v1/users/42"
```

## 発展

`base` や `path` にすでにクエリ文字列が含まれていたらどう扱うべきか、仕様を決めて実装してください。

## 参考

- [urllib パッケージを使ってインターネット上のリソースを取得するには](https://docs.python.org/ja/3.14/howto/urllib2.html)
