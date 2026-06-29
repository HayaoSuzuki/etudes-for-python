---
title: "080: 「withの内側だけ時間を測る」の解答"
description: "contextmanagerとfinallyでwithブロックの経過時間を記録する。"
difficulty: 4
---

# 080: 「withの内側だけ時間を測る」の解答

[問題](../problems/080-contextmanager-timer.md) / [ヒント](../hints/080-contextmanager-timer.md)

**難易度:** ☆☆☆☆

## 方針

`@contextmanager` を使うと、ジェネレータ関数からコンテキストマネージャを作れます。
`yield` の前で開始時刻を取り、`yield` で辞書を呼び出し側へ渡し、`finally` で終了時刻を取ります。

`finally` に置くことで、`with` ブロック内で例外が起きた場合でも経過時間を記録できます。

## 実装

```python
from contextlib import contextmanager
from time import perf_counter


@contextmanager
def elapsed_timer(clock=None):
    if clock is None:
        clock = perf_counter

    timer = {"elapsed": None}
    start = clock()
    try:
        yield timer
    finally:
        end = clock()
        timer["elapsed"] = end - start
```

## 確認

```python
ticks = iter([10.0, 12.5])
with elapsed_timer(lambda: next(ticks)) as timer:
    assert timer["elapsed"] is None

assert timer["elapsed"] == 2.5

ticks = iter([1.0, 1.25])
try:
    with elapsed_timer(lambda: next(ticks)) as failed_timer:
        raise RuntimeError("failed")
except RuntimeError:
    pass

assert failed_timer["elapsed"] == 0.25
```

## 発展

実際の計測では、結果を辞書ではなく小さなクラスにすると、`timer.elapsed` のように属性として読めます。
ただし、その場合でも `finally` で値を更新する構造は同じです。

## 参考

- [contextlib](https://docs.python.org/ja/3.14/library/contextlib.html)

