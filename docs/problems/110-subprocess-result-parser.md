---
title: "110: 外のコマンドの返事を読む"
description: "subprocess.runで外部コマンドを実行し、終了コードと出力を整理する。"
difficulty: 4
---

# 110: 外のコマンドの返事を読む

[ヒント](../hints/110-subprocess-result-parser.md) / [解答](../solutions/110-subprocess-result-parser.md)

**難易度:** ☆☆☆☆

## 問題

関数 `run_command(args)` を書いてください。

この関数は、外部コマンドを実行し、終了コード、標準出力、標準エラーを辞書にまとめます。

## 制約

- `subprocess.run` を使ってください。
- `args` は文字列のリストです。
- シェルを経由してはいけません。
- 標準出力と標準エラーを捕捉してください。
- 文字列として扱ってください。
- コマンドの終了コードが0でなくても、例外を送出しないでください。
- 戻り値は、キー `ok`、`returncode`、`stdout`、`stderr` を持つ辞書です。
- `stdout` と `stderr` は、行ごとのリストにしてください。

## 例

```python
>>> import sys
>>> result = run_command([sys.executable, "-c", "print('ok')"])
>>> result["ok"]
True
>>> result["stdout"]
['ok']
```

## 発展

タイムアウトを指定できるようにしてください。

## 参考

- [subprocess](https://docs.python.org/ja/3.14/library/subprocess.html)
