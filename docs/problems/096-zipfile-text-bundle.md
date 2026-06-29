---
title: "096: 文字列たちをZIPに束ねる"
description: "zipfileで複数のテキストをメモリ上のZIPファイルへまとめる。"
difficulty: 4
---

# 096: 文字列たちをZIPに束ねる

[ヒント](../hints/096-zipfile-text-bundle.md) / [解答](../solutions/096-zipfile-text-bundle.md)

**難易度:** ☆☆☆☆

## 問題

関数 `make_text_zip(files)` と `read_text_zip(data)` を書いてください。

`make_text_zip` は、ファイル名から本文への辞書を受け取り、メモリ上にZIPファイルを作ってバイト列で返します。
`read_text_zip` は、そのバイト列を読み、ファイル名から本文への辞書へ戻します。

## 制約

- `zipfile.ZipFile` を使ってください。
- 実ファイルを作らず、メモリ上で処理してください。
- 本文はUTF-8で扱ってください。
- `make_text_zip` は、ファイル名の昇順でZIPへ追加してください。
- `read_text_zip` は、ディレクトリ項目を無視してください。
- 戻り値の辞書は、ファイル名の昇順に作ってください。

## 例

```python
>>> data = make_text_zip({"b.txt": "B", "a.txt": "A"})
>>> read_text_zip(data)
{'a.txt': 'A', 'b.txt': 'B'}
```

## 発展

圧縮方式や圧縮レベルを引数で指定できるようにしてください。

## 参考

- [zipfile](https://docs.python.org/ja/3.14/library/zipfile.html)
