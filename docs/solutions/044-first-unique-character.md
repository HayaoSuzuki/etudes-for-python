---
title: "044: 「一度だけ現れる声」の解答"
description: "文字列の中で最初に一度だけ現れる文字を探す。"
difficulty: 3
---

# 044: 「一度だけ現れる声」の解答

[問題](../problems/044-first-unique-character.md) / [ヒント](../hints/044-first-unique-character.md)

**難易度:** ☆☆☆

## 方針

1回目のループで、文字ごとの出現回数を辞書に記録します。
2回目のループで元の順番を保ちながら調べ、回数が1の文字を最初に見つけたところで返します。

## 実装

```python
def first_unique_char(text):
    counts = {}
    for ch in text:
        if ch in counts:
            counts[ch] += 1
        else:
            counts[ch] = 1

    for ch in text:
        if counts[ch] == 1:
            return ch
    return None
```

## 確認

```python
assert first_unique_char("swiss") == "w"
assert first_unique_char("aabbc") == "c"
assert first_unique_char("aabb") is None
assert first_unique_char("Aa") == "A"
```

## 発展

大文字と小文字を区別しない場合は、数えるときのキーを `ch.lower()` にします。
ただし、返す文字は元の文字列中の文字にするのか、小文字にそろえるのかを先に決めてください。
