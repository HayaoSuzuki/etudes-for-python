---
title: "089: 「型はふるまいを見ている」のヒント"
description: "typing.Protocolでrenderメソッドを持つ値を受け取る関数を型付けする。"
difficulty: 4
---

# 089: 「型はふるまいを見ている」のヒント

[問題](../problems/089-typing-protocol-duck.md) / [解答](../solutions/089-typing-protocol-duck.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    `Protocol` は、継承しているかどうかではなく、必要なメソッドや属性を持つかどうかを型として表します。

??? tip "ヒント2"

    `Renderable` には、`render(self) -> str` というメソッドだけを書きます。
    実装本体は `...` でかまいません。

??? tip "ヒント3"

    通常の `Protocol` は、`isinstance` では使えません。
    実行時にも判定したい場合は、`@runtime_checkable` を付けます。

??? tip "ヒント4"

    `render_all` は、`Iterable[Renderable]` を受け取り、`list[str]` を返す関数として型付けできます。
    実装は、各要素の `render()` を呼んでリストにするだけです。
