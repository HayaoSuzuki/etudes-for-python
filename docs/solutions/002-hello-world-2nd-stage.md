---
title: "002: Hello world 2nd stageの解答"
description: "sys.stdin.readline()とsys.stdout.write()で標準入出力を扱う。"
difficulty: 2
---

# 002: Hello world 2nd stageの解答

[問題](../problems/002-hello-world-2nd-stage.md) / [ヒント](../hints/002-hello-world-2nd-stage.md)

**難易度:** ☆☆

## 方針

`input()` は標準入力を読む関数であり、`print()` は標準出力へ書く関数です。
この問題では、その背後にある標準入力と標準出力を直接扱います。

標準入力は `sys.stdin`、標準出力は `sys.stdout` で参照できます。
1行を読み、行末だけを取り除き、出力したい文字列を `sys.stdout.write()` に渡します。

## 実装

```python
import sys

name = sys.stdin.readline().rstrip("\r\n")
sys.stdout.write(f"hello, {name}!\n")
```

## 確認

入力:

```text
Ada
```

出力:

```text
hello, Ada!
```

## 補足

`sys.stdout.write()` は、渡された文字列をそのまま書きます。
そのため、出力を1行にするには末尾の `\n` も自分で含めます。
