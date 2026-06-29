---
title: "004: 月初月締"
description: "argparseで売上レポート用の引数を解析し、検証済みの設定辞書を作る。"
difficulty: 1
---

# 004: 月初月締

[ヒント](../hints/004-argparse-flags.md) / [解答](../solutions/004-argparse-flags.md)

**難易度:** ☆
## 問題

関数 `parse_sales_args(args)` を書いてください。
この関数は、売上レポートを作るコマンドライン引数を解析し、設定辞書を返します。

扱う引数は次のとおりです。

- 位置引数 `csv_path`
- 必須オプション `--month`。値は `YYYY-MM` 形式
- 任意オプション `--format`。値は `table` または `json`。省略時は `table`
- 任意オプション `--tax-rate`。0以上の整数。省略時は `10`
- 任意フラグ `--include-zero`。指定されたときだけ `True`

戻り値は、キー `csv_path`、`month`、`format`、`tax_rate`、`include_zero` を持つ辞書にしてください。

## 制約

- `argparse.ArgumentParser` を使ってください。
- `args` は文字列のリストです。
- `--month` が `YYYY-MM` 形式でない場合は、`argparse` のエラーとして扱ってください。
- `--tax-rate` が負の場合も、`argparse` のエラーとして扱ってください。
- 不正な引数では `argparse` の通常どおり `SystemExit` が送出されてかまいません。

## 例

```python
>>> parse_sales_args(["sales.csv", "--month", "2026-06"])
{'csv_path': 'sales.csv', 'month': '2026-06', 'format': 'table', 'tax_rate': 10, 'include_zero': False}
>>> parse_sales_args(["sales.csv", "--month", "2026-06", "--format", "json", "--tax-rate", "8", "--include-zero"])
{'csv_path': 'sales.csv', 'month': '2026-06', 'format': 'json', 'tax_rate': 8, 'include_zero': True}
```

## 発展

`--sort total` と `--sort name` を追加し、レポートの並び順も引数で指定できるようにしてください。

## 参考

- [Argparse チュートリアル](https://docs.python.org/ja/3.14/howto/argparse.html)