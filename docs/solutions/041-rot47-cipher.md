---
title: "041: 「メリー・ポピンズからの暗号文」の解答"
description: "印字可能ASCII文字を47文字ずらして復号する。"
difficulty: 2
---

# 041: 「メリー・ポピンズからの暗号文」の解答

[問題](../problems/041-rot47-cipher.md) / [ヒント](../hints/041-rot47-cipher.md)

**難易度:** ☆☆

## 方針

ROT47は、ASCIIコード33から126までの94文字を対象にします。
対象範囲の先頭を0として扱い、47を足して94で割った余りを取ります。

この変換は暗号化と復号で同じです。
暗号文にもう一度ROT47をかけると平文に戻ります。

## 実装

```python
def rot47(text: str) -> str:
    result = []

    for char in text:
        code = ord(char)

        if 33 <= code <= 126:
            rotated = 33 + ((code - 33 + 47) % 94)
            result.append(chr(rotated))
        else:
            result.append(char)

    return "".join(result)
```

## 確認

```python
ciphertext = "$FA6C42=:7C28:=:DE:46IA:2=:5@4:@FD"
plaintext = "Supercalifragilisticexpialidocious"

assert rot47(ciphertext) == plaintext
assert rot47(plaintext) == ciphertext
assert rot47(rot47(plaintext)) == plaintext
```

## 平文

```text
Supercalifragilisticexpialidocious
```

題材は、映画『メリー・ポピンズ』の楽曲に登場する語 [Supercalifragilisticexpialidocious](https://en.wikipedia.org/wiki/Supercalifragilisticexpialidocious) です。

## 参考

- [ROT13: ROT47](https://ja.wikipedia.org/wiki/ROT13#ROT47)
