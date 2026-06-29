---
title: "085: 「図形は面積を約束する」のヒント"
description: "abc.ABCとabstractmethodで図形の共通インターフェースを定義する。"
difficulty: 4
---

# 085: 「図形は面積を約束する」のヒント

[問題](../problems/085-abc-shape-area.md) / [解答](../solutions/085-abc-shape-area.md)

**難易度:** ☆☆☆☆

??? tip "ヒント1"

    抽象基底クラスは、具象クラスが実装すべきメソッドを示すために使えます。

??? tip "ヒント2"

    `class Shape(ABC):` とし、`area` に `@abstractmethod` を付けます。
    抽象メソッドを実装しないクラスはインスタンス化できません。

??? tip "ヒント3"

    `Rectangle.area()` は `width * height`、`Circle.area()` は `math.pi * radius ** 2` です。

??? tip "ヒント4"

    `total_area` は、受け取った図形の `area()` を順に呼び、その合計を返します。

