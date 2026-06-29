---
title: "095: 「INIの旗を読む」のヒント"
description: "configparserでINI形式の設定を読み、機能フラグを真偽値へ変換する。"
difficulty: 3
---

# 095: 「INIの旗を読む」のヒント

[問題](../problems/095-configparser-feature-flags.md) / [解答](../solutions/095-configparser-feature-flags.md)

**難易度:** ☆☆☆

??? tip "ヒント1"

    `ConfigParser` は、INI形式の文字列をセクションとキーに分けて読みます。
    文字列から読む場合は `read_string` を使います。

??? tip "ヒント2"

    セクションがあるかどうかは、`parser.has_section("features")` で確認できます。

??? tip "ヒント3"

    真偽値として読むには `getboolean` が使えます。
    対応していない値では `ValueError` が送出されます。

??? tip "ヒント4"

    キーの並びを安定させるため、`sorted(parser["features"])` でキーを昇順に処理します。
    各キーに対して `parser.getboolean("features", key)` を呼びます。
