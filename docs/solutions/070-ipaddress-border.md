---
title: "070: 「住所の外へ出る者を見つけろ」の解答"
description: "ipaddressを使って、IPアドレスがネットワーク内にあるか分類する。"
difficulty: 3
---

# 070: 「住所の外へ出る者を見つけろ」の解答

[問題](../problems/070-ipaddress-border.md) / [ヒント](../hints/070-ipaddress-border.md)

**難易度:** ☆☆☆

## 方針

ネットワークとアドレスを `ipaddress` のオブジェクトに変換します。
変換に失敗した候補は `invalid` に入れ、バージョン違いまたは範囲外の候補は `outside` に入れます。

## 実装

```python
import ipaddress


def split_addresses(cidr, candidates):
    network = ipaddress.ip_network(cidr, strict=False)
    result = {
        "inside": [],
        "outside": [],
        "invalid": [],
    }

    for text in candidates:
        try:
            address = ipaddress.ip_address(text)
        except ValueError:
            result["invalid"].append(text)
            continue

        if address.version == network.version and address in network:
            result["inside"].append(text)
        else:
            result["outside"].append(text)

    return result
```

## 確認

```python
assert split_addresses("192.168.0.0/24", [
    "192.168.0.10",
    "192.168.1.10",
    "2001:db8::1",
    "not address",
]) == {
    "inside": ["192.168.0.10"],
    "outside": ["192.168.1.10", "2001:db8::1"],
    "invalid": ["not address"],
}
```

## 発展

`outside` を、同じIPバージョンで範囲外のものと、IPバージョンが違うものに分けてください。

## 参考

- [ipaddressモジュールの紹介](https://docs.python.org/ja/3.14/howto/ipaddress.html)
