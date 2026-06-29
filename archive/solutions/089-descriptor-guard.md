---
title: "089: 「番人は属性の入口に立つ」の解答"
description: "デスクリプタで属性代入を検査し、インスタンスごとに値を保存する。"
difficulty: 5
---

# 089: 「番人は属性の入口に立つ」の解答

[問題](../problems/089-descriptor-guard.md) / [ヒント](../hints/089-descriptor-guard.md)

**難易度:** ☆☆☆☆☆

## 方針

`__set_name__` で属性名を受け取り、インスタンス側に保存する名前を作ります。
`__set__` で型と範囲を検査し、検査を通った値だけをインスタンスに保存します。

## 実装

```python
class NonNegativeInteger:
    def __set_name__(self, owner, name):
        self.storage_name = f"_{name}"

    def __get__(self, instance, owner):
        if instance is None:
            return self
        return getattr(instance, self.storage_name)

    def __set__(self, instance, value):
        if type(value) is not int:
            raise TypeError("value must be an int")
        if value < 0:
            raise ValueError("value must be non-negative")
        setattr(instance, self.storage_name, value)


class CartLine:
    quantity = NonNegativeInteger()
    unit_price = NonNegativeInteger()

    def __init__(self, name, quantity, unit_price):
        self.name = name
        self.quantity = quantity
        self.unit_price = unit_price

    @property
    def total(self):
        return self.quantity * self.unit_price
```

## 確認

```python
pen = CartLine("pen", 2, 120)
notebook = CartLine("notebook", 1, 300)
pen.quantity = 5

assert pen.total == 600
assert notebook.total == 300

try:
    pen.quantity = -1
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")

try:
    pen.unit_price = True
except TypeError:
    pass
else:
    raise AssertionError("TypeError was not raised")
```

## 発展

上限も検査できる `IntegerRange(minimum, maximum)` に一般化してください。

## 参考

- [デスクリプタ ガイド](https://docs.python.org/ja/3.14/howto/descriptor.html)

