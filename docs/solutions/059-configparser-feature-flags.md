---
title: "059: 「INIの旗を読む」の解答"
description: "ConfigParserでfeaturesセクションを読み、getbooleanで真偽値へ変換する。"
difficulty: 3
---

# 059: 「INIの旗を読む」の解答

[問題](../problems/059-configparser-feature-flags.md) / [ヒント](../hints/059-configparser-feature-flags.md)

**難易度:** ☆☆☆

## 方針

`ConfigParser` にINI文字列を読み込ませます。
`features` セクションがなければ空の辞書を返します。

値の変換には `getboolean` を使います。
`getboolean` は、`yes`、`no`、`on`、`off`、`1`、`0` などを真偽値へ変換します。

## 実装

```python
import configparser


def read_feature_flags(ini_text):
    parser = configparser.ConfigParser()
    parser.read_string(ini_text)

    if not parser.has_section("features"):
        return {}

    return {
        key: parser.getboolean("features", key)
        for key in sorted(parser["features"])
    }
```

## 確認

```python
assert read_feature_flags("[features]\nsearch = yes\ncache = off\n") == {
    "cache": False,
    "search": True,
}
assert read_feature_flags("[server]\nport = 8000\n") == {}

try:
    read_feature_flags("[features]\nsearch = maybe\n")
except ValueError:
    pass
else:
    raise AssertionError("ValueError was not raised")
```

## 発展

`ConfigParser` は既定でキーを小文字化します。
キーの大文字小文字を保持したい場合は、`optionxform` の扱いを調べてください。

## 参考

- [configparser](https://docs.python.org/ja/3.14/library/configparser.html)

