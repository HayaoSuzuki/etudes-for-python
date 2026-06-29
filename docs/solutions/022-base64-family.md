---
title: "022: 「64文字の手紙」の解答"
description: "3バイトを24ビットの整数にし、6ビットずつBase64の文字に変換する。"
difficulty: 5
---

# 022: 「64文字の手紙」の解答

[問題](../problems/022-base64-family.md) / [ヒント](../hints/022-base64-family.md)

**難易度:** ☆☆☆☆☆

## 方針

エンコードでは、入力を3バイトずつ処理します。
3バイトを24ビットの整数にし、上位から6ビットずつ取り出して、Base64のアルファベットを引きます。

最後のかたまりが3バイトに満たない場合は、足りないぶんを0で埋めてから同じ計算をします。
その後、足したバイト数に応じて末尾を `=` に置き換えます。

デコードでは、4文字を6ビットずつの値に戻します。
`=` は値0として計算し、最後に取り出すバイト数を調整します。

## 実装

```python
STANDARD_ALPHABET = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
URLSAFE_ALPHABET = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789-_"


def validate_alphabet(alphabet: str) -> None:
    if len(alphabet) != 64:
        raise ValueError("alphabet must contain 64 characters")
    if len(set(alphabet)) != 64:
        raise ValueError("alphabet must not contain duplicate characters")
    if "=" in alphabet:
        raise ValueError("alphabet must not contain '='")


def base64_encode(
    data: bytes,
    alphabet: str = STANDARD_ALPHABET,
    padding: bool = True,
) -> str:
    validate_alphabet(alphabet)

    encoded = []

    for start in range(0, len(data), 3):
        chunk = data[start : start + 3]
        missing = 3 - len(chunk)
        block = int.from_bytes(chunk + b"\x00" * missing, "big")

        indexes = [
            (block >> 18) & 0b111111,
            (block >> 12) & 0b111111,
            (block >> 6) & 0b111111,
            block & 0b111111,
        ]
        chars = [alphabet[index] for index in indexes]

        if missing:
            chars[-missing:] = "=" * missing

        encoded.extend(chars)

    result = "".join(encoded)
    if not padding:
        result = result.rstrip("=")
    return result


def base64_decode(text: str, alphabet: str = STANDARD_ALPHABET) -> bytes:
    validate_alphabet(alphabet)

    if len(text) % 4 == 1:
        raise ValueError("invalid Base64 length")

    first_padding = text.find("=")
    if first_padding != -1:
        if text[first_padding:] != "=" * (len(text) - first_padding):
            raise ValueError("invalid padding position")
        if len(text) % 4 != 0:
            raise ValueError("padded Base64 length must be a multiple of 4")

    padded_text = text + "=" * ((4 - len(text) % 4) % 4)
    table = {char: index for index, char in enumerate(alphabet)}
    decoded = bytearray()

    for start in range(0, len(padded_text), 4):
        chunk = padded_text[start : start + 4]
        padding_count = chunk.count("=")

        if padding_count > 2:
            raise ValueError("invalid padding length")

        values = []
        for char in chunk:
            if char == "=":
                values.append(0)
            elif char in table:
                values.append(table[char])
            else:
                raise ValueError(f"invalid Base64 character: {char!r}")

        block = (
            (values[0] << 18)
            | (values[1] << 12)
            | (values[2] << 6)
            | values[3]
        )
        decoded.extend(
            [
                (block >> 16) & 0xFF,
                (block >> 8) & 0xFF,
                block & 0xFF,
            ][: 3 - padding_count]
        )

    return bytes(decoded)
```

## 確認

```python
assert base64_encode(b"") == ""
assert base64_encode(b"f") == "Zg=="
assert base64_encode(b"fo") == "Zm8="
assert base64_encode(b"foo") == "Zm9v"
assert base64_encode(b"hello") == "aGVsbG8="

assert base64_decode("") == b""
assert base64_decode("Zg==") == b"f"
assert base64_decode("Zm8=") == b"fo"
assert base64_decode("Zm9v") == b"foo"
assert base64_decode("aGVsbG8=") == b"hello"

assert base64_encode(b"\xfb\xff") == "+/8="
assert base64_encode(b"\xfb\xff", URLSAFE_ALPHABET) == "-_8="
assert base64_encode(b"\xfb\xff", URLSAFE_ALPHABET, padding=False) == "-_8"
assert base64_decode("-_8", URLSAFE_ALPHABET) == b"\xfb\xff"

for sample in (b"", b"f", b"fo", b"foo", b"hello", bytes(range(256))):
    assert base64_decode(base64_encode(sample)) == sample

for invalid in ("A", "====", "Zm=9", "Zm9v="):
    try:
        base64_decode(invalid)
    except ValueError:
        pass
    else:
        raise AssertionError(f"{invalid!r} must raise ValueError")
```

## 考え方

Base64の本体は、文字列処理ではなくビット列の分割です。
3バイトを24ビットの整数としてまとめると、6ビット単位で値を取り出せます。

標準 Base64 と URL-safe Base64 の違いは、62番目と63番目の文字だけです。
アルファベットを引数にすると、同じ実装で複数の変種を扱えます。