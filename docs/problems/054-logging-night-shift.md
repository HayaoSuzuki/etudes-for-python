---
title: "054: printはもう夜勤しない"
description: "loggingでログ出力を組み立てる。"
difficulty: 3
---

# 054: printはもう夜勤しない

[ヒント](../hints/054-logging-night-shift.md) / [解答](../solutions/054-logging-night-shift.md)

**難易度:** ☆☆☆

## 問題

関数 `make_task_logger(stream)` と `log_task_result(logger, task_name, ok)` を書いてください。

`make_task_logger` は、名前が `tasks` のロガーを返します。
このロガーは、渡された `stream` に次の形式でログを書き込みます。

```text
LEVEL:tasks:message
```

`log_task_result` は、タスクが成功したときに `INFO`、失敗したときに `WARNING` のログを出します。

## 制約

- `print` は使わず、`logging` を使ってください。
- `make_task_logger` を複数回呼んでも、同じログが重複して出ないようにしてください。
- `log_task_result(logger, "backup", True)` は `finished backup` を出力します。
- `log_task_result(logger, "sync", False)` は `failed sync` を出力します。

## 例

```python
>>> import io
>>> stream = io.StringIO()
>>> logger = make_task_logger(stream)
>>> log_task_result(logger, "backup", True)
>>> log_task_result(logger, "sync", False)
>>> stream.getvalue().splitlines()
['INFO:tasks:finished backup', 'WARNING:tasks:failed sync']
```

## 参考

- [Logging HOWTO](https://docs.python.org/ja/3.14/howto/logging.html)

