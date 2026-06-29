---
title: "008: 「二で割り切れる者たち」のヒント"
description: "整数のリストから偶数だけを取り出す。"
difficulty: 2
---

# 008: 「二で割り切れる者たち」のヒント

[問題](../problems/008-even-numbers.md) / [解答](../solutions/008-even-numbers.md)

**難易度:** ☆☆

??? tip "ヒント1"

    偶数は2で割った余りが0になる整数です。

??? tip "ヒント2"

    結果用の空リストを作り、条件を満たす数だけ追加します。

??? tip "ヒント3"

    `if number % 2 == 0:` の中で `result.append(number)` を呼び出します。

