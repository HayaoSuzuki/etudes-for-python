---
title: "027: 「空白を脱いだ名前」の解答"
description: "文字列の前後の空白を取り除き、あいさつ文を作る。"
difficulty: 1
---

# 027: 「空白を脱いだ名前」の解答

[問題](../problems/027-trimmed-greeting.md) / [ヒント](../hints/027-trimmed-greeting.md)

**難易度:** ☆

## 方針

まず `strip()` で前後の空白を取り除きます。
その結果が空文字列なら、表示用の名前を `ゲスト` に置き換えます。
最後に文字列を連結して返します。

## 実装

```python
def greet(name):
    name = name.strip()
    if name == "":
        name = "ゲスト"
    return "こんにちは、" + name + "さん"
```

## 確認

```python
assert greet("Alice") == "こんにちは、Aliceさん"
assert greet("  Python  ") == "こんにちは、Pythonさん"
assert greet("山田 太郎") == "こんにちは、山田 太郎さん"
assert greet("   ") == "こんにちは、ゲストさん"
```

## 発展

英字の名前だけを扱うなら、`capitalize()` で先頭だけ大文字にできます。
ただし、日本語名や複数語の名前では期待どおりとは限りません。
