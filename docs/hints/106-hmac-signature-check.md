---
title: "106: 「署名は一定時間で比べる」のヒント"
description: "hmacでメッセージ署名を作り、compare_digestで検証する。"
difficulty: 4
---

# 106: 「署名は一定時間で比べる」のヒント

[問題](../problems/106-hmac-signature-check.md) / [解答](../solutions/106-hmac-signature-check.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    HMACは、秘密鍵とメッセージから署名を作る仕組みです。
    同じ秘密鍵とメッセージなら同じ署名になります。

??? tip "ヒント2"

    `hmac.new(secret, message, hashlib.sha256)` でHMACオブジェクトを作れます。
    `hexdigest()` で16進文字列にします。

??? tip "ヒント3"

    検証では、受け取った署名と、自分で計算した署名を比較します。

??? tip "ヒント4"

    署名の比較では、通常の `==` ではなく `hmac.compare_digest` を使います。
    これは比較にかかる時間から情報が漏れにくい比較関数です。
