---
title: "018: 「列車が到着する前に」の解答"
description: "逆ポーランド記法の式を列挙し、通常ルールでは10を作れない組み合わせを調べる。"
---

# 018: 「列車が到着する前に」の解答

[問題](../problems/018-ten-puzzle.md) / [ヒント](../hints/018-ten-puzzle.md)

## 方針

4個の数字と3個の演算子からなる逆ポーランド記法の式を全探索します。
逆ポーランド記法では、計算順がトークンの並びに含まれるため、括弧の文字列を作る必要がありません。

4個の数値を `N`、3個の演算子を `O` と書くと、正しい逆ポーランド記法の形は5通りです。
この形に、数字の順列と演算子の組み合わせを流し込みます。

割り算を含むので、評価には `Fraction` を使います。
0で割る候補は失敗として扱い、別の候補の探索を続けます。

## 実装

```python
from fractions import Fraction
from itertools import combinations_with_replacement, permutations, product


TARGET = Fraction(10)
OPERATORS = ("+", "-", "*", "/")
RPN_PATTERNS = (
    "NNONONO",
    "NNONNOO",
    "NNNONOO",
    "NNNOONO",
    "NNNNOOO",
)


def make_rpn_expression(
    numbers: tuple[int, ...], operators: tuple[str, ...], pattern: str
) -> tuple[str, ...]:
    number_iter = iter(numbers)
    operator_iter = iter(operators)
    tokens = []

    for kind in pattern:
        if kind == "N":
            tokens.append(str(next(number_iter)))
        else:
            tokens.append(next(operator_iter))

    return tuple(tokens)


def rpn_expressions(digits: tuple[int, ...]):
    for numbers in sorted(set(permutations(digits))):
        for operators in product(OPERATORS, repeat=3):
            for pattern in RPN_PATTERNS:
                yield make_rpn_expression(numbers, operators, pattern)


def evaluate_rpn_exact(tokens: tuple[str, ...]) -> Fraction | None:
    stack = []

    for token in tokens:
        if token in OPERATORS:
            right = stack.pop()
            left = stack.pop()

            if token == "+":
                stack.append(left + right)
            elif token == "-":
                stack.append(left - right)
            elif token == "*":
                stack.append(left * right)
            elif right == 0:
                return None
            else:
                stack.append(left / right)
        else:
            stack.append(Fraction(int(token)))

    return stack.pop()


def can_make_ten(digits: tuple[int, ...]) -> bool:
    return any(evaluate_rpn_exact(expression) == TARGET for expression in rpn_expressions(digits))


def format_digits(digits: tuple[int, ...]) -> str:
    return "".join(str(digit) for digit in digits)


def unsolvable_ten_puzzle_combinations() -> list[str]:
    return [
        format_digits(digits)
        for digits in combinations_with_replacement(range(10), 4)
        if not can_make_ten(digits)
    ]


def main() -> None:
    for digits in unsolvable_ten_puzzle_combinations():
        print(digits)


if __name__ == "__main__":
    main()
```

## 確認

```python
assert evaluate_rpn_exact(("1", "2", "+", "3", "*", "4", "+")) == 13
assert can_make_ten((1, 3, 5, 8))
assert not can_make_ten((1, 1, 1, 1))

unsolved = unsolvable_ten_puzzle_combinations()

assert len(unsolved) == 163
assert unsolved[:5] == ["0000", "0001", "0002", "0003", "0004"]
assert unsolved[-3:] == ["7888", "7999", "8899"]
assert "1111" in unsolved
assert "1358" not in unsolved
```

## 考え方

`RPN_PATTERNS` は、4個の数値と3個の演算子から作れる正しい逆ポーランド記法の形です。
たとえば `NNONONO` は、2個の数値を演算して、その結果と次の数値を演算する形です。

`rpn_expressions` は、数字の順列、演算子3個の組み合わせ、RPNの形を組み合わせて候補式を作ります。
同じ数字が重複すると同じ順列が出るので、`set(permutations(digits))` で重複を取り除きます。

`evaluate_rpn_exact` は、前問で作った評価器と同じスタック評価です。
テンパズルでは割り算を含むため、`Fraction` を使って10と正確に比較します。

## 参考

- [テンパズル](https://ja.wikipedia.org/wiki/%E3%83%86%E3%83%B3%E3%83%91%E3%82%BA%E3%83%AB)
