---
title: "065: 「printはもう夜勤しない」のヒント"
description: "loggingのLogger、Handler、Formatterを使ってログ出力を組み立てる。"
difficulty: 3
---

# 065: 「printはもう夜勤しない」のヒント

[問題](../problems/065-logging-night-shift.md) / [解答](../solutions/065-logging-night-shift.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `logging.getLogger("tasks")` で名前付きロガーを取得できます。

??? tip "ヒント2"

    指定されたストリームに出すには `logging.StreamHandler(stream)` を使います。
    出力形式は `logging.Formatter` で設定します。

??? tip "ヒント3"

    同じロガーにハンドラを追加し続けると、1回のログが複数回出ます。
    作り直す前に既存のハンドラを消す方法を考えてください。

??? tip "ヒント4"

    `logger.info("finished %s", task_name)` のように、値はログ呼び出しの引数として渡せます。
