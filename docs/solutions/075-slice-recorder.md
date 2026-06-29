---
title: "075: 「スライスは切らずに渡される」の解答"
description: "__getitem__に渡されるsliceオブジェクトとタプル添字を観察する。"
difficulty: 4
---

# 075: 「スライスは切らずに渡される」の解答

[問題](../problems/075-slice-recorder.md) / [ヒント](../hints/075-slice-recorder.md)

**難易度:** ☆☆☆☆

## 方針

`__getitem__` が受け取ったキーを、補助関数で変換します。
キーが `slice` なら `start`、`stop`、`step` を取り出します。
キーがタプルなら、各要素を同じ規則で変換します。

## 実装

```python
class SliceRecorder:
    def __getitem__(self, key):
        return self._record(key)

    def _record(self, key):
        if isinstance(key, slice):
            return ("slice", key.start, key.stop, key.step)
        if isinstance(key, tuple):
            recorded = []
            for item in key:
                recorded.append(self._record(item))
            return tuple(recorded)
        return key
```

## 確認

```python
recorder = SliceRecorder()
assert recorder[3] == 3
assert recorder[1:5:2] == ("slice", 1, 5, 2)
assert recorder[:3] == ("slice", None, 3, None)
assert recorder[1:4, "x", ::-1] == (("slice", 1, 4, None), "x", ("slice", None, None, -1))
```

## 発展

`recorder[1,]` の返り値を確認してください。
カンマが1つだけでも、添字はタプルになります。

## 参考

- [Python言語リファレンス](https://docs.python.org/ja/3.14/reference/expressions.html#slicings)

