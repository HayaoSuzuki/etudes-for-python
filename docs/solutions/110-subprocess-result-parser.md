---
title: "110: 「外のコマンドの返事を読む」の解答"
description: "subprocess.runをshellなしで実行し、出力を行ごとのリストへ整える。"
difficulty: 4
---

# 110: 「外のコマンドの返事を読む」の解答

[問題](../problems/110-subprocess-result-parser.md) / [ヒント](../hints/110-subprocess-result-parser.md)

**難易度:** ☆☆☆☆

## 方針

`subprocess.run` に引数リストを渡して実行します。
`capture_output=True` で標準出力と標準エラーを捕捉し、`text=True` で文字列として受け取ります。

終了コードが0でない場合も辞書にまとめるため、`check=False` にします。

## 実装

```python
import subprocess


def run_command(args):
    completed = subprocess.run(
        args,
        capture_output=True,
        text=True,
        check=False,
    )
    return {
        "ok": completed.returncode == 0,
        "returncode": completed.returncode,
        "stdout": completed.stdout.splitlines(),
        "stderr": completed.stderr.splitlines(),
    }
```

## 確認

```python
import sys


result = run_command([sys.executable, "-c", "print('ok')"])

assert result["ok"] is True
assert result["returncode"] == 0
assert result["stdout"] == ["ok"]
assert result["stderr"] == []
```

## 発展

外部コマンドの実行では、タイムアウト、環境変数、作業ディレクトリ、入力の渡し方も仕様になります。
必要な範囲だけを引数として公開します。

## 参考

- [subprocess](https://docs.python.org/ja/3.14/library/subprocess.html)
