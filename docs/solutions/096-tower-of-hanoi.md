---
title: "096: 「終焉のカウントダウン」の解答"
description: "再帰で小さい塔の移動手順を組み合わせる。"
difficulty: 3
---

# 096: 「終焉のカウントダウン」の解答

[問題](../problems/096-tower-of-hanoi.md) / [ヒント](../hints/096-tower-of-hanoi.md)

**難易度:** ☆☆☆

## 方針

`n` 枚の円盤を `start` から `goal` へ移す問題を考えます。
上の `n - 1` 枚を `spare` へ退避し、一番大きい円盤を `goal` へ移し、退避した `n - 1` 枚を `goal` へ戻します。

この3段階のうち、1段階目と3段階目は同じ形の小さい問題です。
そのため、再帰関数で書けます。

## 実装

```python
def hanoi_moves(n: int, start: str = "A", goal: str = "C", spare: str = "B") -> list[str]:
    if n < 0:
        raise ValueError("n must be non-negative")
    if n == 0:
        return []

    moves = []
    moves.extend(hanoi_moves(n - 1, start, spare, goal))
    moves.append(f"{start} -> {goal}")
    moves.extend(hanoi_moves(n - 1, spare, goal, start))
    return moves


def main() -> None:
    n = int(input())

    for move in hanoi_moves(n):
        print(move)


if __name__ == "__main__":
    main()
```

## 確認

```python
assert hanoi_moves(0) == []
assert hanoi_moves(1) == ["A -> C"]
assert hanoi_moves(2) == ["A -> B", "A -> C", "B -> C"]
assert hanoi_moves(3) == [
    "A -> C",
    "A -> B",
    "C -> B",
    "A -> C",
    "B -> A",
    "B -> C",
    "A -> C",
]
assert len(hanoi_moves(10)) == 2**10 - 1
```

## 考え方

`hanoi_moves(n - 1, start, spare, goal)` は、上の `n - 1` 枚を作業用の杭へ移します。
ここで `goal` は作業用の杭として使われます。

一番大きい円盤を `start` から `goal` へ移したあと、`hanoi_moves(n - 1, spare, goal, start)` で退避した円盤を目的の杭へ移します。
この順序を守ると、大きい円盤を小さい円盤の上に置かずに済みます。

## 参考

- [ハノイの塔](https://ja.wikipedia.org/wiki/%E3%83%8F%E3%83%8E%E3%82%A4%E3%81%AE%E5%A1%94)

