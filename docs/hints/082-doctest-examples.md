---
title: "082: 「例はそのまま試験になる」のヒント"
description: "doctestで対話形式の実行例を検査し、試行数と失敗数を返す。"
difficulty: 3
---

# 082: 「例はそのまま試験になる」のヒント

[問題](../problems/082-doctest-examples.md) / [解答](../solutions/082-doctest-examples.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `doctest` は、`>>>` で始まる対話形式の例を読み取り、実際に実行して期待される出力と比べます。

??? tip "ヒント2"

    文字列からテストを作るには、`DocTestParser` が使えます。
    `get_doctest` に、実行用の名前空間、名前、ファイル名、開始行を渡します。

??? tip "ヒント3"

    テストを実行するには `DocTestRunner` を使います。
    `runner.run(test)` の戻り値には、試行数と失敗数が入っています。

??? tip "ヒント4"

    失敗内容を表示したくない場合は、`runner.run(test, out=lambda text: None)` のように出力先を差し替えます。
    呼び出し側の辞書を変更しないように、名前空間はコピーして渡すと扱いやすくなります。
