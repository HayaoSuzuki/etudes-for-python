

---
title: "070: 住所の外へ出る者を見つけろ"
description: "ipaddressを使って、IPアドレスがネットワーク内にあるか分類する。"
difficulty: 3
---

# 070: 住所の外へ出る者を見つけろ

[ヒント](../hints/070-ipaddress-border.md) / [解答](../solutions/070-ipaddress-border.md)

**難易度:** ☆☆☆

## 問題

関数 `split_addresses(cidr, candidates)` を書いてください。
この関数は、候補の文字列をIPアドレスとして解釈し、指定されたネットワークの内側、外側、不正な値に分類します。

戻り値は、キー `inside`、`outside`、`invalid` を持つ辞書です。
各リストには、入力された文字列をそのまま入れてください。

## 制約

- `ipaddress` モジュールを使ってください。
- `cidr` は `192.168.0.0/24` のようなネットワーク表記です。
- `candidates` は文字列のリストです。
- IPv4ネットワークに対するIPv6アドレス、またはその逆は `outside` に入れてください。
- 候補がIPアドレスとして解釈できない場合は `invalid` に入れてください。

## 例

```python
>>> split_addresses("192.168.0.0/24", [
...     "192.168.0.10",
...     "192.168.1.10",
...     "2001:db8::1",
...     "not address",
... ])
{'inside': ['192.168.0.10'], 'outside': ['192.168.1.10', '2001:db8::1'], 'invalid': ['not address']}
```

## 参考

- [ipaddressモジュールの紹介](https://docs.python.org/ja/3.14/howto/ipaddress.html)
