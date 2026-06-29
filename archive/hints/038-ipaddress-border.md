---
title: "038: 「住所の外へ出る者を見つけろ」のヒント"
description: "ipaddressを使って、IPアドレスがネットワーク内にあるか分類する。"
difficulty: 3
---

# 038: 「住所の外へ出る者を見つけろ」のヒント

[問題](../problems/038-ipaddress-border.md) / [解答](../solutions/038-ipaddress-border.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    ネットワークは `ipaddress.ip_network(cidr, strict=False)` で作れます。

??? tip "ヒント2"

    候補のアドレスは `ipaddress.ip_address(text)` で作れます。
    不正な文字列では `ValueError` が送出されます。

??? tip "ヒント3"

    IPアドレスがネットワークに含まれるかは `address in network` で調べられます。

??? tip "ヒント4"

    IPv4とIPv6が混ざったときは、`address.version` と `network.version` を比べてから分類すると意図が明確になります。

