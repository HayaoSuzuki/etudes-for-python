---
title: "046: 「コメントはそのままHTMLにしない」の解答"
description: "html.escapeで投稿者名と本文をエスケープしてHTML断片を作る。"
difficulty: 3
---

# 046: 「コメントはそのままHTMLにしない」の解答

[問題](../problems/046-html-escape-comment.md) / [ヒント](../hints/046-html-escape-comment.md)

**難易度:** ☆☆☆

## 方針

投稿者名と本文はどちらも外から来る文字列として扱います。
HTMLへ埋め込む前に、それぞれ `html.escape` でエスケープします。

## 実装

```python
from html import escape


def render_comment(author, text):
    safe_author = escape(author, quote=True)
    safe_text = escape(text, quote=True)
    return f"<p><strong>{safe_author}</strong>: {safe_text}</p>"
```

## 確認

```python
assert render_comment("<Admin>", '5 > 3 & "ok"') == (
    "<p><strong>&lt;Admin&gt;</strong>: "
    "5 &gt; 3 &amp; &quot;ok&quot;</p>"
)
```

## 発展

HTMLを生成する処理では、どの値がすでにエスケープ済みかを混同しないことが重要です。
二重にエスケープすると表示が崩れ、エスケープし忘れると危険なHTMLになります。

## 参考

- [html](https://docs.python.org/ja/3.14/library/html.html)

