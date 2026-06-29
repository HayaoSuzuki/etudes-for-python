---
title: "004: 「売上レポートの入口を作る」の解答"
description: "ArgumentParserに引数仕様と検証関数を登録し、Namespaceを辞書へ変換する。"
difficulty: 1
---

# 004: 「売上レポートの入口を作る」の解答

[問題](../problems/004-argparse-flags.md) / [ヒント](../hints/004-argparse-flags.md)

**難易度:** ☆
## 方針

`ArgumentParser` に、位置引数、必須オプション、選択式オプション、真偽フラグを登録します。

`--month` と `--tax-rate` は、文字列を受け取って検査する関数を `type` に渡します。
検査に失敗したら `ArgumentTypeError` を送出すると、`argparse` のエラーメッセージとして扱われます。

## 実装

```python
import argparse


def month_text(text):
    if len(text) != 7 or text[4] != "-":
        raise argparse.ArgumentTypeError("month must be YYYY-MM")
    year_text = text[:4]
    month_part = text[5:]
    if not year_text.isdigit() or not month_part.isdigit():
        raise argparse.ArgumentTypeError("month must be YYYY-MM")
    month = int(month_part)
    if not 1 <= month <= 12:
        raise argparse.ArgumentTypeError("month must be between 01 and 12")
    return text


def non_negative_int(text):
    try:
        value = int(text)
    except ValueError as exc:
        raise argparse.ArgumentTypeError("expected int") from exc
    if value < 0:
        raise argparse.ArgumentTypeError("expected non-negative int")
    return value


def build_sales_parser():
    parser = argparse.ArgumentParser(prog="sales-report")
    parser.add_argument("csv_path")
    parser.add_argument("--month", required=True, type=month_text)
    parser.add_argument("--format", choices=["table", "json"], default="table")
    parser.add_argument("--tax-rate", type=non_negative_int, default=10)
    parser.add_argument("--include-zero", action="store_true")
    return parser


def parse_sales_args(args):
    namespace = build_sales_parser().parse_args(args)
    return vars(namespace)
```

## 確認

```python
assert parse_sales_args(["sales.csv", "--month", "2026-06"]) == {
    "csv_path": "sales.csv",
    "month": "2026-06",
    "format": "table",
    "tax_rate": 10,
    "include_zero": False,
}
assert parse_sales_args([
    "sales.csv",
    "--month", "2026-06",
    "--format", "json",
    "--tax-rate", "8",
    "--include-zero",
]) == {
    "csv_path": "sales.csv",
    "month": "2026-06",
    "format": "json",
    "tax_rate": 8,
    "include_zero": True,
}
```

## 発展

並び順を増やす場合は、`parser.add_argument("--sort", choices=[...])` を追加します。
ここで返した設定辞書を、CSV集計の関数へ渡せば、CLI部分と集計部分を分けて実装できます。

## 参考

- [Argparse チュートリアル](https://docs.python.org/ja/3.14/howto/argparse.html)