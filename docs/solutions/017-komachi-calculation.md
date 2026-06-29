---
title: "017: 「百夜通い」の解答"
description: "候補式を逆ポーランド記法へ変換し、分数で正確に100と比較する。"
difficulty: 5
---

# 017: 「百夜通い」の解答

[問題](../problems/017-komachi-calculation.md) / [ヒント](../hints/017-komachi-calculation.md)

**難易度:** ☆☆☆☆☆

## 方針

数字の間に入れるものは、8か所それぞれで5通りあります。
`itertools.product` を使うと、すべての組み合わせを作れます。

各組み合わせから、空白区切りの中置記法の式を作ります。
その式を `infix_to_rpn` で逆ポーランド記法へ変換し、`Fraction` を使う評価器で100と比較します。

## 実装

```python
from fractions import Fraction
from itertools import product


PRECEDENCE = {
    "+": 1,
    "-": 1,
    "*": 2,
    "/": 2,
}
TARGET = Fraction(100)
DIGITS = "123456789"
OPERATORS = ("", "+", "-", "*", "/")


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


def evaluate_rpn_exact(expression: str) -> Fraction:
    stack = []

    for token in expression.split():
        if token in PRECEDENCE:
            right = stack.pop()
            left = stack.pop()

            if token == "+":
                stack.append(left + right)
            elif token == "-":
                stack.append(left - right)
            elif token == "*":
                stack.append(left * right)
            else:
                stack.append(left / right)
        else:
            stack.append(Fraction(int(token)))

    return stack.pop()


def make_expression(operators: tuple[str, ...]) -> str:
    parts = []
    number = DIGITS[0]

    for operator, digit in zip(operators, DIGITS[1:]):
        if operator == "":
            number += digit
        else:
            parts.append(number)
            parts.append(operator)
            number = digit

    parts.append(number)
    return " ".join(parts)


def komachi_solutions() -> list[str]:
    solutions = []

    for operators in product(OPERATORS, repeat=8):
        expression = make_expression(operators)
        rpn = infix_to_rpn(expression)

        if evaluate_rpn_exact(rpn) == TARGET:
            solutions.append(f"{expression} = 100")

    return solutions


def main() -> None:
    for expression in komachi_solutions():
        print(expression)


if __name__ == "__main__":
    main()
```

## 確認

```python
assert infix_to_rpn("123 + 45 - 67 + 8 - 9") == "123 45 + 67 - 8 + 9 -"
assert infix_to_rpn("1 / 2 / 3 * 456 + 7 + 8 + 9") == "1 2 / 3 / 456 * 7 + 8 + 9 +"
assert evaluate_rpn_exact("1 2 / 3 / 456 * 7 + 8 + 9 +") == 100

solutions = komachi_solutions()

assert len(solutions) == 101
assert solutions[0] == "123 + 45 - 67 + 8 - 9 = 100"
assert solutions[-1] == "1 / 2 / 3 * 456 + 7 + 8 + 9 = 100"
assert "123 - 45 - 67 + 89 = 100" in solutions
assert "1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 * 9 = 100" in solutions
```

## 考え方

`make_expression` は、演算子の組み合わせから中置記法の式を作ります。
「何も入れない」を選んだ場所では、数字を文字列として連結します。

`infix_to_rpn` は、通常の演算順位を反映した逆ポーランド記法へ変換します。
そのため、`komachi_solutions` は、候補式の生成と判定だけに集中できます。

`evaluate_rpn_exact` は、前問で作った評価器と同じスタック処理です。
違いは、スタックに `float` ではなく `Fraction` を積むことです。

## 参考

- [小町算](https://ja.wikipedia.org/wiki/%E5%B0%8F%E7%94%BA%E7%AE%97)
