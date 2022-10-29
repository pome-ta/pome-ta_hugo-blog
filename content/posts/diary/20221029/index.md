---
title: "objc_util を調査してみる"
date: 2022-10-29
categories: ["diary", "Pythonista3"]
tags: ["Python", "objc_util"]
menu: main
---

# Pythonista3 のobjc_util モジュール調査

Pythonista3 に入っている`objc_util.py` を写経しつつ構造の理解をすすめる

## 調査

- `objc_util.py` そのもの
- rubicon-objc
  - [beeware/rubicon-objc: A bridge interface between Python and Objective-C.](https://github.com/beeware/rubicon-objc)
  - [Rubicon Objective-C — Rubicon 0.4.2 documentation](https://rubicon-objc.readthedocs.io/en/latest/index.html)
  - [rubicon-objc · PyPI](https://pypi.org/project/rubicon-objc/)

## 現状

macOS で実行(`import ui` をコメントアウト) すると、`NSString` など、エラー吐く

Python2系 での分岐があるけども、基本3系のみを想定とした書き方にする

### `ObjCClass` を実装

`cdll,LoadLibrary` に、名前入れると呼べる？

3系だと、`.encode('ascii')` で変換が必要なんかな？

`NSObject`, `b'NSObject'` こんな感じになるのね

#### `ctypes.cdll.LoadLibrary` ってどう呼び出してる？

引数を直で書き込めているけど、どこから取得して呼び出してるんか？

[cdll | ctypes --- Pythonのための外部関数ライブラリ — Python 3.9.12 ドキュメント](https://docs.python.org/ja/3.9/library/ctypes.html#ctypes.CDLL)

[LoadLibrary | ctypes --- Pythonのための外部関数ライブラリ — Python 3.9.12 ドキュメント](https://docs.python.org/ja/3.9/library/ctypes.html#ctypes.LibraryLoader.LoadLibrary)

共有ライブラリ場所？

### わからないところ

`LP64` => `True` を返す
