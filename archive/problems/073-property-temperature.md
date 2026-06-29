---
title: "073: 温度は二つの単位を持つ"
description: "propertyで摂氏と華氏を相互変換し、絶対零度未満を拒否する。"
difficulty: 3
---

# 073: 温度は二つの単位を持つ

[ヒント](../hints/073-property-temperature.md) / [解答](../solutions/073-property-temperature.md)

**難易度:** ☆☆☆

## 問題

クラス `Temperature` を書いてください。

`Temperature` は内部では摂氏で温度を保持し、`celsius` と `fahrenheit` のどちらでも読み書きできるようにします。

## 制約

- `property` を使ってください。
- `Temperature(celsius=0)` のように初期化できるようにしてください。
- `celsius` に値を代入すると、摂氏として保存してください。
- `fahrenheit` に値を代入すると、華氏から摂氏へ変換して保存してください。
- 摂氏で絶対零度 `-273.15` 未満になる値は `ValueError` を送出してください。
- 読み取り時の `fahrenheit` は、摂氏から計算してください。

## 例

```python
>>> temp = Temperature(celsius=0)
>>> temp.fahrenheit
32.0
>>> temp.fahrenheit = 212
>>> temp.celsius
100.0
>>> temp.celsius = -300
Traceback (most recent call last):
...
ValueError: temperature is below absolute zero
```

## 発展

ケルビンでも読み書きできるプロパティを追加してください。

## 参考

- [property](https://docs.python.org/ja/3.14/library/functions.html#property)

