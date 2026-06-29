---
title: "097: 非同期の結果を順に集める"
description: "asyncio.gatherで複数の非同期処理を実行し、入力順に結果を返す。"
difficulty: 4
---

# 097: 非同期の結果を順に集める

[ヒント](../hints/097-asyncio-gather-results.md) / [解答](../solutions/097-asyncio-gather-results.md)

**難易度:** ☆☆☆☆

## 問題

非同期関数 `run_jobs(jobs)` を書いてください。

`jobs` は、引数なしで呼び出すと await 可能な値を返す関数のリストです。
`run_jobs` は、すべてのジョブを実行し、結果を入力順のリストで返します。

## 制約

- `asyncio.gather` を使ってください。
- `jobs` の各要素は、引数なしで呼び出せる関数です。
- ジョブは順に待つのではなく、まとめて開始してください。
- 戻り値は、各ジョブの結果を入力順に並べたリストです。
- いずれかのジョブが例外を送出した場合は、その例外を呼び出し側へ送出してかまいません。

## 例

```python
>>> import asyncio
>>> async def value(n):
...     await asyncio.sleep(0)
...     return n
...
>>> asyncio.run(run_jobs([lambda: value(1), lambda: value(2)]))
[1, 2]
```

## 発展

失敗したジョブの例外も結果リストに入れて返すモードを追加してください。

## 参考

- [asyncio.gather](https://docs.python.org/ja/3.14/library/asyncio-task.html#asyncio.gather)
