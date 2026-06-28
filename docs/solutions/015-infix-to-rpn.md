---
title: "015: 「そして逆ポーランド記法へ」の解答"
description: "演算子スタックを使って中置記法を逆ポーランド記法へ変換する。"
---

# 015: 「そして逆ポーランド記法へ」の解答

[問題](../problems/015-infix-to-rpn.md) / [ヒント](../hints/015-infix-to-rpn.md)

## 方針

出力用のリストと、演算子用のスタックを使います。
数値はすぐに出力へ追加します。

演算子は、優先順位を見てからスタックに積みます。
新しい演算子よりも先に計算すべき演算子がスタックの上にあれば、それを出力へ移します。

## 実装

```python
PRECEDENCE = {
    "+": 1,
    "-": 1,
    "*": 2,
    "/": 2,
}


def infix_to_rpn(expression: str) -> str:
    output = []
    operators = []

    for token in expression.split():
        if token in PRECEDENCE:
            while (
                operators
                and operators[-1] in PRECEDENCE
                and PRECEDENCE[operators[-1]] >= PRECEDENCE[token]
            ):
                output.append(operators.pop())
            operators.append(token)
        elif token == "(":
            operators.append(token)
        elif token == ")":
            while operators and operators[-1] != "(":
                output.append(operators.pop())
            operators.pop()
        else:
            output.append(token)

    while operators:
        output.append(operators.pop())

    return " ".join(output)
```

## 確認

```python
assert infix_to_rpn("3 + 4") == "3 4 +"
assert infix_to_rpn("3 + 4 * 2") == "3 4 2 * +"
assert infix_to_rpn("( 3 + 4 ) * 2") == "3 4 + 2 *"
assert infix_to_rpn("5 + ( 1 + 2 ) * 4 - 3") == "5 1 2 + 4 * + 3 -"
assert infix_to_rpn("3 + 4 * 2 / ( 1 - 5 )") == "3 4 2 * 1 5 - / +"
```

## 考え方

`*` や `/` は、`+` や `-` より先に出力へ移す必要があります。
そのため、演算子を読んだ時点で、スタック上の演算子の優先順位を確認します。

同じ優先順位の演算子は左から右へ結合します。
そのため、スタック上の演算子の優先順位が同じ場合も、先に出力へ移します。

括弧の内側は、外側より先に計算されます。
`)` を読んだときに `(` までの演算子を出力へ移すと、括弧内の式がまとまります。

## 参考

- [中置記法](https://ja.wikipedia.org/wiki/%E4%B8%AD%E7%BD%AE%E8%A8%98%E6%B3%95)
