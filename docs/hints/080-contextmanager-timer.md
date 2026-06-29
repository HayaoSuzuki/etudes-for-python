---
title: "080: 「withの内側だけ時間を測る」のヒント"
description: "contextlib.contextmanagerで処理時間を測るコンテキストマネージャを作る。"
difficulty: 4
---

# 080: 「withの内側だけ時間を測る」のヒント

[問題](../problems/080-contextmanager-timer.md) / [解答](../solutions/080-contextmanager-timer.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `@contextmanager` を付けた関数では、`yield` より前が `with` ブロックに入る前、`yield` より後がブロックを出た後に実行されます。

??? tip "ヒント2"

    `with ... as timer:` に渡したい値を `yield timer` のように返します。
    今回は `{"elapsed": None}` という辞書を渡します。

??? tip "ヒント3"

    経過時間は、開始時刻と終了時刻の差です。
    `clock` が `None` のときだけ `time.perf_counter` を使います。

??? tip "ヒント4"

    ブロック内で例外が起きても記録するには、`try` と `finally` を使います。
    `yield` を `try` の中に置き、`finally` で終了時刻を読みます。

