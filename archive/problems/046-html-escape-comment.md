---
title: "046: コメントはそのままHTMLにしない"
description: "html.escapeでユーザー入力をエスケープし、HTML断片を作る。"
difficulty: 3
---

# 046: コメントはそのままHTMLにしない

[ヒント](../hints/046-html-escape-comment.md) / [解答](../solutions/046-html-escape-comment.md)

**難易度:** ☆☆☆

## 問題

関数 `render_comment(author, text)` を書いてください。

この関数は、投稿者名と本文を受け取り、HTML断片を返します。

## 制約

- `html.escape` を使ってください。
- `author` と `text` は文字列です。
- 投稿者名と本文の両方をエスケープしてください。
- ダブルクォートもエスケープしてください。
- 戻り値は `<p><strong>投稿者</strong>: 本文</p>` の形にしてください。

## 例

```python
>>> render_comment("<Admin>", '5 > 3 & "ok"')
'<p><strong>&lt;Admin&gt;</strong>: 5 &gt; 3 &amp; &quot;ok&quot;</p>'
```

## 発展

本文中の改行を `<br>` に変換してください。

## 参考

- [html](https://docs.python.org/ja/3.14/library/html.html)

