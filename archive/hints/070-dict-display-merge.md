---
title: "070: 「最後に置いた鍵が勝つ」のヒント"
description: "辞書表示の評価順と重複キーの規則に合わせて値を統合する。"
difficulty: 3
---

# 070: 「最後に置いた鍵が勝つ」のヒント

[問題](../problems/070-dict-display-merge.md) / [解答](../solutions/070-dict-display-merge.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    結果用の空の辞書を作り、`parts` を左から右へ処理します。

??? tip "ヒント2"

    `item` なら、そのキーに値を代入します。

??? tip "ヒント3"

    `mapping` なら、含まれるキーと値を順に代入します。後から代入した値が残ります。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#dictionary-displays)

