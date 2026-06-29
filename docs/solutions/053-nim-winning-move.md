---
title: "053: 「石の上にもニム」の解答"
description: "ニム和が0になるように、1つの山を減らす。"
difficulty: 4
---

# 053: 「石の上にもニム」の解答

[問題](../problems/053-nim-winning-move.md) / [ヒント](../hints/053-nim-winning-move.md)

**難易度:** ☆☆☆☆

## 方針

各山の石数をすべて排他的論理和で畳み込みます。
この値をニム和と呼びます。

ニム和が0なら、現在のプレイヤーに必勝手はありません。
ニム和が0でなければ、1つの山を減らしてニム和0の局面を作れます。

山の石数を `pile`、ニム和を `s` とします。
`target = pile ^ s` が `pile` より小さい山を見つけ、その山を `target` 個に減らします。
この手を打つと、相手に渡す盤面のニム和は0になります。

## 実装

```python
def nim_sum(piles: list[int]) -> int:
    result = 0
    for pile in piles:
        if pile < 0:
            raise ValueError("pile sizes must be non-negative")
        result ^= pile
    return result


def winning_move(piles: list[int]) -> tuple[int, int] | None:
    total = nim_sum(piles)
    if total == 0:
        return None

    for index, pile in enumerate(piles):
        target = pile ^ total
        if target < pile:
            return index, target

    raise RuntimeError("unreachable")
```

## 確認

```python
def apply_move(piles: list[int], move: tuple[int, int]) -> list[int]:
    index, new_count = move
    after = piles.copy()
    after[index] = new_count
    return after


assert winning_move([3, 4, 5]) == (0, 1)
assert winning_move([1, 2, 3]) is None
assert winning_move([7]) == (0, 0)
assert winning_move([10, 12, 15]) == (0, 3)
assert winning_move([]) is None

for piles in ([3, 4, 5], [7], [10, 12, 15], [1, 1, 2, 7]):
    move = winning_move(piles)
    assert move is not None
    assert nim_sum(apply_move(piles, move)) == 0
```

## 考え方

ニム和が0の局面を相手に渡せれば、相手がどの山を減らしてもニム和は0でなくなります。
その後、自分の手番で再びニム和0の局面を作れます。

`target = pile ^ total` が現在の石数より小さい山を選べば、1つの山だけを合法的に減らせます。
新しい盤面のニム和は、元のニム和 `total` と、変更前の `pile` と、変更後の `target` を打ち消し合うため0になります。
