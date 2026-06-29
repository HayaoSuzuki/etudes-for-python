---
title: "059: INIの旗を読む"
description: "configparserでINI形式の設定を読み、機能フラグを真偽値へ変換する。"
difficulty: 3
---

# 059: INIの旗を読む

[ヒント](../hints/059-configparser-feature-flags.md) / [解答](../solutions/059-configparser-feature-flags.md)

**難易度:** ☆☆☆

## 問題

関数 `read_feature_flags(ini_text)` を書いてください。

この関数は、INI形式の文字列から `[features]` セクションを読み、機能名から真偽値への辞書を返します。

## 制約

- `configparser.ConfigParser` を使ってください。
- `[features]` セクションがない場合は空の辞書を返してください。
- 値は `true`、`false`、`yes`、`no`、`on`、`off`、`1`、`0` のいずれかとします。
- 値は大文字小文字を区別しません。
- 不正な真偽値がある場合は `ValueError` を送出してください。
- 戻り値のキーはアルファベット順に並べてください。

## 例

```python
>>> read_feature_flags("[features]\\nsearch = yes\\ncache = off\\n")
{'cache': False, 'search': True}
>>> read_feature_flags("[server]\\nport = 8000\\n")
{}
```

## 発展

`[features.local]` のような環境別セクションで既定値を上書きできるようにしてください。

## 参考

- [configparser](https://docs.python.org/ja/3.14/library/configparser.html)

