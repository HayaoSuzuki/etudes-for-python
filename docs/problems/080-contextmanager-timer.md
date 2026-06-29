---
title: "080: withの内側だけ時間を測る"
description: "contextlib.contextmanagerで処理時間を測るコンテキストマネージャを作る。"
difficulty: 4
---

# 080: withの内側だけ時間を測る

[ヒント](../hints/080-contextmanager-timer.md) / [解答](../solutions/080-contextmanager-timer.md)

**難易度:** ☆☆☆☆

## 問題

関数 `elapsed_timer(clock=None)` を書いてください。

この関数は、`with` 文で使えるコンテキストマネージャを返します。
`with` ブロックに入ってから出るまでの経過時間を、辞書の `elapsed` に保存してください。

## 制約

- `contextlib.contextmanager` を使ってください。
- `clock` が `None` の場合は、`time.perf_counter` を使ってください。
- `clock` が渡された場合は、その関数を時刻取得に使ってください。
- `with elapsed_timer(...) as timer:` の `timer` は辞書です。
- ブロック内では `timer["elapsed"]` は `None` です。
- ブロックを出たあと、`timer["elapsed"]` は終了時刻と開始時刻の差になります。
- ブロック内で例外が起きても、`elapsed` は記録してください。

## 例

```python
>>> ticks = iter([10.0, 12.5])
>>> with elapsed_timer(lambda: next(ticks)) as timer:
...     timer["elapsed"] is None
True
>>> timer["elapsed"]
2.5
```

## 発展

経過時間を秒ではなくミリ秒で返すオプションを追加してください。

## 参考

- [contextlib](https://docs.python.org/ja/3.14/library/contextlib.html)

