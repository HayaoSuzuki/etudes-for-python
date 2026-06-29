---
title: "065: 「printはもう夜勤しない」の解答"
description: "loggingのLogger、Handler、Formatterを使ってログ出力を組み立てる。"
difficulty: 3
---

# 065: 「printはもう夜勤しない」の解答

[問題](../problems/065-logging-night-shift.md) / [ヒント](../hints/065-logging-night-shift.md)

**難易度:** ☆☆☆

## 方針

名前付きロガーに `StreamHandler` を付け、`Formatter` で出力形式を決めます。
`make_task_logger` を何度呼んでもログが重複しないように、既存のハンドラを消してから追加します。

## 実装

```python
import logging


def make_task_logger(stream):
    logger = logging.getLogger("tasks")
    logger.setLevel(logging.INFO)
    logger.propagate = False
    logger.handlers.clear()

    handler = logging.StreamHandler(stream)
    handler.setFormatter(logging.Formatter("%(levelname)s:%(name)s:%(message)s"))
    logger.addHandler(handler)
    return logger


def log_task_result(logger, task_name, ok):
    if ok:
        logger.info("finished %s", task_name)
    else:
        logger.warning("failed %s", task_name)
```

## 確認

```python
import io

stream = io.StringIO()
logger = make_task_logger(stream)
log_task_result(logger, "backup", True)
log_task_result(logger, "sync", False)

assert stream.getvalue().splitlines() == [
    "INFO:tasks:finished backup",
    "WARNING:tasks:failed sync",
]
```

## 発展

`DEBUG` ログも出せるようにするには、ロガーとハンドラのどちらのレベルを変える必要があるかを確認してください。

## 参考

- [Logging HOWTO](https://docs.python.org/ja/3.14/howto/logging.html)
