---
title: "042: 「ASCIIは二度回る」の解答"
description: "ASCIIコード33から126までを94文字の輪として扱う。"
difficulty: 3
---

# 042: 「ASCIIは二度回る」の解答

[問題](../problems/042-rotate-printable-ascii.md) / [ヒント](../hints/042-rotate-printable-ascii.md)

**難易度:** ☆☆☆

## 方針

`!` から `~` までの文字を、94文字の輪として扱います。
文字コードから `ord("!")` を引くと、先頭を0とする番号に変換できます。

その番号に `shift` を足し、94で割った余りを取ります。
最後に `ord("!")` を足し戻すと、回転後の文字コードになります。

## 実装

```python
def rotate_printable_ascii(text: str, shift: int) -> str:
    result = []
    start = ord("!")
    end = ord("~")
    size = end - start + 1

    for char in text:
        code = ord(char)

        if start <= code <= end:
            rotated = start + ((code - start + shift) % size)
            result.append(chr(rotated))
        else:
            result.append(char)

    return "".join(result)
```

## 確認

```python
ciphertext = "$FA6C42=:7C28:=:DE:46IA:2=:5@4:@FD"
plaintext = "Supercalifragilisticexpialidocious"

assert rotate_printable_ascii("Hello", 47) == "w6==@"
assert rotate_printable_ascii("w6==@", 47) == "Hello"
assert rotate_printable_ascii("!", -1) == "~"
assert rotate_printable_ascii("Hello, World!", 94) == "Hello, World!"
assert rotate_printable_ascii(ciphertext, 47) == plaintext
assert rotate_printable_ascii(plaintext, 47) == ciphertext
```

## 考え方

`shift` が94の倍数であれば、対象文字は元の文字に戻ります。
これは、対象範囲が94文字だからです。

また、負の `shift` を特別扱いする必要はありません。
Pythonの剰余演算を使うと、左回転も同じ式で扱えます。
