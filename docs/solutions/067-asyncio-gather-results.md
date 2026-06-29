---
title: "067: 「非同期の結果を順に集める」の解答"
description: "asyncio.gatherで複数のawait可能な値をまとめて待つ。"
difficulty: 4
---

# 067: 「非同期の結果を順に集める」の解答

[問題](../problems/067-asyncio-gather-results.md) / [ヒント](../hints/067-asyncio-gather-results.md)

**難易度:** ☆☆☆☆

## 方針

各ジョブを呼び出して、await 可能な値を作ります。
それらを `asyncio.gather` にまとめて渡すと、並行して実行され、結果は渡した順序で返ります。

問題の仕様ではリストを返すため、`gather` の結果を `list` に変換します。

## 実装

```python
import asyncio


async def run_jobs(jobs):
    awaitables = [job() for job in jobs]
    return list(await asyncio.gather(*awaitables))
```

## 確認

```python
async def value(n):
    await asyncio.sleep(0)
    return n


assert asyncio.run(run_jobs([lambda: value(1), lambda: value(2)])) == [1, 2]
```

## 発展

`asyncio.gather` には `return_exceptions=True` というオプションがあります。
これを使うと、ジョブが送出した例外を結果リストの要素として受け取れます。

## 参考

- [asyncio.gather](https://docs.python.org/ja/3.14/library/asyncio-task.html#asyncio.gather)

