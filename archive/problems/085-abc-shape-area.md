---
title: "085: 図形は面積を約束する"
description: "abc.ABCとabstractmethodで図形の共通インターフェースを定義する。"
difficulty: 4
---

# 085: 図形は面積を約束する

[ヒント](../hints/085-abc-shape-area.md) / [解答](../solutions/085-abc-shape-area.md)

**難易度:** ☆☆☆☆

## 問題

抽象基底クラス `Shape`、具象クラス `Rectangle` と `Circle`、関数 `total_area(shapes)` を書いてください。

`Shape` は、面積を返す `area()` メソッドを持つ図形を表します。

## 制約

- `abc.ABC` と `abc.abstractmethod` を使ってください。
- `Shape.area(self)` は抽象メソッドにしてください。
- `Rectangle(width, height)` は幅と高さを受け取ります。
- `Circle(radius)` は半径を受け取ります。
- 幅、高さ、半径が0以下の場合は `ValueError` を送出してください。
- `total_area(shapes)` は、各図形の面積の合計を返してください。

## 例

```python
>>> rect = Rectangle(3, 4)
>>> rect.area()
12
>>> round(Circle(2).area(), 2)
12.57
>>> round(total_area([rect, Circle(1)]), 2)
15.14
```

## 発展

周長を返す抽象メソッドも追加してください。

## 参考

- [abc](https://docs.python.org/ja/3.14/library/abc.html)

