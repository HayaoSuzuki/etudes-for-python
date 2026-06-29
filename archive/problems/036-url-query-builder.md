---
title: "036: URLはクエリを背負って走る"
description: "urllib.parseでURLとクエリ文字列を組み立てる。"
difficulty: 2
---

# 036: URLはクエリを背負って走る

[ヒント](../hints/036-url-query-builder.md) / [解答](../solutions/036-url-query-builder.md)

**難易度:** ☆☆

## 問題

関数 `build_url(base, path, params)` を書いてください。
この関数は、基底URL、相対パス、クエリパラメータからURLを組み立てます。

## 制約

- `urllib.parse.urljoin` と `urllib.parse.urlencode` を使ってください。
- `params` が空なら、末尾に `?` を付けないでください。
- `params` の値がリストの場合、同じキーを複数回出してください。
- 空白や日本語はURL用にエンコードしてください。
- 実際のHTTP通信は行いません。

## 例

```python
>>> build_url("https://api.example.com/v1/", "search", {"q": "猫 Python", "tag": ["howto", "stdlib"]})
'https://api.example.com/v1/search?q=%E7%8C%AB+Python&tag=howto&tag=stdlib'
>>> build_url("https://api.example.com/v1/", "users/42", {})
'https://api.example.com/v1/users/42'
```

## 参考

- [urllib パッケージを使ってインターネット上のリソースを取得するには](https://docs.python.org/ja/3.14/howto/urllib2.html)

