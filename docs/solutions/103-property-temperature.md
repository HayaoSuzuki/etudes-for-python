---
title: "103: 「温度は二つの単位を持つ」の解答"
description: "摂氏を内部状態にし、propertyのsetterで検査と変換を行う。"
difficulty: 3
---

# 103: 「温度は二つの単位を持つ」の解答

[問題](../problems/103-property-temperature.md) / [ヒント](../hints/103-property-temperature.md)

**難易度:** ☆☆☆

## 方針

内部状態は摂氏だけにします。
華氏は、読み取り時に摂氏から計算し、代入時に摂氏へ変換します。

絶対零度の検査は `celsius` の setter に集めます。

## 実装

```python
class Temperature:
    ABSOLUTE_ZERO = -273.15

    def __init__(self, celsius=0):
        self.celsius = celsius

    @property
    def celsius(self):
        return self._celsius

    @celsius.setter
    def celsius(self, value):
        value = float(value)
        if value < self.ABSOLUTE_ZERO:
            raise ValueError("temperature is below absolute zero")
        self._celsius = value

    @property
    def fahrenheit(self):
        return self.celsius * 9 / 5 + 32

    @fahrenheit.setter
    def fahrenheit(self, value):
        self.celsius = (float(value) - 32) * 5 / 9
```

## 確認

```python
temp = Temperature(celsius=0)

assert temp.fahrenheit == 32.0
temp.fahrenheit = 212
assert temp.celsius == 100.0

try:
    temp.celsius = -300
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

状態を1つに絞ると、複数の単位を扱っても値の不整合が起きにくくなります。
ケルビンを追加する場合も、内部状態は摂氏のままで十分です。

## 参考

- [property](https://docs.python.org/ja/3.14/library/functions.html#property)
