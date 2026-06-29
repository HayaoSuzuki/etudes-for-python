---
title: "003: Hello world 2nd stage"
description: "print()とinput()を使わず、標準入力から読んだ名前を標準出力へ書く。"
difficulty: 2
---

# 003: Hello world 2nd stage

[ヒント](../hints/003-hello-world-2nd-stage.md) / [解答](../solutions/003-hello-world-2nd-stage.md)

**難易度:** ☆☆

## 問題

名前を1行受け取り、`hello, name!` の形で出力するPythonスクリプトを書いてください。

ただし、`print()` と `input()` は使えません。
標準入力から読み、標準出力へ書いてください。

## 入力

標準入力から、名前を表す文字列が1行与えられます。
行末の改行は名前に含めません。

```text
Alice
```

## 出力

標準出力へ、あいさつを1行で出力します。

```text
hello, Alice!
```

## 制約

- Python標準ライブラリだけを使います。
- `print()` と `input()` を呼び出してはいけません。
- 名前そのものに含まれる空白は残します。

## 例

入力:

```text
Grace
```

出力:

```text
hello, Grace!
```
