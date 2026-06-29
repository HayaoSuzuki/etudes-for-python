---
title: "064: 旗を立てれば設定が歩く"
description: "argparseでコマンドライン引数を解析し、設定辞書に変換する。"
difficulty: 3
---

# 064: 旗を立てれば設定が歩く

[ヒント](../hints/064-argparse-flags.md) / [解答](../solutions/064-argparse-flags.md)

**難易度:** ☆☆☆

## 問題

関数 `parse_resize_args(args)` を書いてください。
この関数は、画像リサイズ用のコマンドライン引数を解析し、設定辞書を返します。

扱う引数は次のとおりです。

- 位置引数 `input`
- 必須オプション `--width`
- 必須オプション `--height`
- 任意オプション `--format`。値は `png` または `jpg`。省略時は `png`
- 任意フラグ `--keep-aspect`。指定されたときだけ `True`

## 制約

- `argparse.ArgumentParser` を使ってください。
- `args` は文字列のリストです。
- `--width` と `--height` は整数として扱います。
- 戻り値は、キー `input`、`width`、`height`、`format`、`keep_aspect` を持つ辞書です。
- 不正な引数では `argparse` の通常どおり `SystemExit` が送出されてかまいません。

## 例

```python
>>> parse_resize_args(["photo.jpg", "--width", "800", "--height", "600"])
{'input': 'photo.jpg', 'width': 800, 'height': 600, 'format': 'png', 'keep_aspect': False}
>>> parse_resize_args(["photo.jpg", "--width", "800", "--height", "600", "--format", "jpg", "--keep-aspect"])
{'input': 'photo.jpg', 'width': 800, 'height': 600, 'format': 'jpg', 'keep_aspect': True}
```

## 参考

- [Argparse チュートリアル](https://docs.python.org/ja/3.14/howto/argparse.html)
