---
title: "102: 「図形は面積を約束する」の解答"
description: "ABCとabstractmethodでareaを必須にし、具象図形で実装する。"
difficulty: 4
---

# 102: 「図形は面積を約束する」の解答

[問題](../problems/102-abc-shape-area.md) / [ヒント](../hints/102-abc-shape-area.md)

**難易度:** ☆☆☆☆

## 方針

`Shape` を抽象基底クラスにし、`area` を抽象メソッドとして定義します。
`Rectangle` と `Circle` は `Shape` を継承し、それぞれの面積計算を実装します。

## 実装

```python
from abc import ABC, abstractmethod
from math import pi


class Shape(ABC):
    @abstractmethod
    def area(self):
        pass


class Rectangle(Shape):
    def __init__(self, width, height):
        if width <= 0 or height <= 0:
            raise ValueError("width and height must be positive")
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height


class Circle(Shape):
    def __init__(self, radius):
        if radius <= 0:
            raise ValueError("radius must be positive")
        self.radius = radius

    def area(self):
        return pi * self.radius ** 2


def total_area(shapes):
    return sum(shape.area() for shape in shapes)
```

## 確認

```python
rect = Rectangle(3, 4)

assert rect.area() == 12
assert round(Circle(2).area(), 2) == 12.57
assert round(total_area([rect, Circle(1)]), 2) == 15.14

try:
    Shape()
except TypeError:
    pass
else:
    raise AssertionError("TypeError was not raised")
```

## 発展

抽象基底クラスは、実装の共有だけでなく、クラスが満たすべき約束を明示するために使えます。
実装を持たない抽象メソッドでも、設計上の意味があります。

## 参考

- [abc](https://docs.python.org/ja/3.14/library/abc.html)
