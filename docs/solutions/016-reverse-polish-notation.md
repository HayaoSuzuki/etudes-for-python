---
title: "016: 「計算機上に実装する電卓」の解答"
description: "数値と演算子を左から読み、スタックで式を評価する。"
---

# 016: 「計算機上に実装する電卓」の解答

[問題](../problems/016-reverse-polish-notation.md) / [ヒント](../hints/016-reverse-polish-notation.md)

## 方針

式を空白で分割し、左から順に処理します。
数値ならスタックに積みます。

演算子なら、スタックから右辺、左辺の順に2つの値を取り出します。
計算結果をスタックへ戻すと、次の計算の被演算子として使えます。

## 実装

```python
def evaluate_rpn(expression: str) -> float:
    stack = []

    for token in expression.split():
        if token in {"+", "-", "*", "/"}:
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
            stack.append(float(token))

    return stack.pop()


def format_result(value: float) -> str:
    if value.is_integer():
        return str(int(value))
    return str(value)


def main() -> None:
    expression = input()
    result = evaluate_rpn(expression)
    print(format_result(result))


if __name__ == "__main__":
    main()
```

## 確認

```python
assert format_result(evaluate_rpn("3 4 +")) == "7"
assert format_result(evaluate_rpn("5 1 2 + 4 * + 3 -")) == "14"
assert format_result(evaluate_rpn("10 4 /")) == "2.5"
assert format_result(evaluate_rpn("2 3 4 * +")) == "14"
assert format_result(evaluate_rpn("-3 4 * 10 +")) == "-2"
```

## 考え方

逆ポーランド記法では、演算子が現れた時点で、その演算子に必要な被演算子が直前にそろっています。
そのため、スタックの末尾から2つ取り出せば計算できます。

`-` と `/` は左右の順序が結果に影響します。
`pop` で先に取り出した値を右辺、次に取り出した値を左辺として扱います。

## 参考

- [逆ポーランド記法](https://ja.wikipedia.org/wiki/%E9%80%86%E3%83%9D%E3%83%BC%E3%83%A9%E3%83%B3%E3%83%89%E8%A8%98%E6%B3%95)
