---
title: "053: 「旗を立てれば設定が歩く」の解答"
description: "argparseで位置引数、必須オプション、選択肢、真偽フラグを扱う。"
difficulty: 3
---

# 053: 「旗を立てれば設定が歩く」の解答

[問題](../problems/053-argparse-flags.md) / [ヒント](../hints/053-argparse-flags.md)

**難易度:** ☆☆☆

## 方針

`ArgumentParser` に引数の仕様を登録し、受け取った `args` を解析します。
真偽フラグは `store_true` を使うと、指定されたときだけ `True` になります。

## 実装

```python
import argparse


def build_resize_parser():
    parser = argparse.ArgumentParser(prog="resize")
    parser.add_argument("input")
    parser.add_argument("--width", type=int, required=True)
    parser.add_argument("--height", type=int, required=True)
    parser.add_argument("--format", choices=["png", "jpg"], default="png")
    parser.add_argument("--keep-aspect", action="store_true")
    return parser


def parse_resize_args(args):
    namespace = build_resize_parser().parse_args(args)
    return vars(namespace)
```

## 確認

```python
assert parse_resize_args(["photo.jpg", "--width", "800", "--height", "600"]) == {
    "input": "photo.jpg",
    "width": 800,
    "height": 600,
    "format": "png",
    "keep_aspect": False,
}
assert parse_resize_args([
    "photo.jpg",
    "--width", "800",
    "--height", "600",
    "--format", "jpg",
    "--keep-aspect",
]) == {
    "input": "photo.jpg",
    "width": 800,
    "height": 600,
    "format": "jpg",
    "keep_aspect": True,
}
```

## 発展

`ArgumentParser` に `description` を渡し、`--help` で表示される説明文を整えてください。

## 参考

- [Argparse チュートリアル](https://docs.python.org/ja/3.14/howto/argparse.html)

