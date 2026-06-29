---
title: "103: 「温度は二つの単位を持つ」のヒント"
description: "propertyで摂氏と華氏を相互変換し、絶対零度未満を拒否する。"
difficulty: 3
---

# 103: 「温度は二つの単位を持つ」のヒント

[問題](../problems/103-property-temperature.md) / [解答](../solutions/103-property-temperature.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    内部では摂氏だけを保存すると、状態が1つに決まりやすくなります。

??? tip "ヒント2"

    `@property` を付けたメソッドは、属性のように読めます。
    `@name.setter` を使うと、代入時の処理を書けます。

??? tip "ヒント3"

    華氏から摂氏への変換は `(fahrenheit - 32) * 5 / 9` です。
    摂氏から華氏への変換は `celsius * 9 / 5 + 32` です。

??? tip "ヒント4"

    絶対零度の検査は、摂氏に変換したあとの値に対して行います。
    `celsius` setter に検査を集めると、初期化でも華氏 setter でも同じ検査を使えます。
