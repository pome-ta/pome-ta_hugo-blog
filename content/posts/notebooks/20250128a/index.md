---
title: '`rubicon-objc` と`toga` と `Pyto` と'
date: 2025-01-28
categories: ['notebook']
tags: ['Python', 'rubicon-objc', 'toga', 'Pyto']
menu: main
draft: false
---

# Pythonista3 以外でも、良い感じにRubicon-objc を動かしたい

## リンク

### rubicon
- [GitHub - beeware/rubicon-objc: A bridge interface between Python and Objective-C.](https://github.com/beeware/rubicon-objc)
  - [Rubicon 0.5.0](https://rubicon-objc.readthedocs.io/en/stable/)

### toga
- [GitHub - beeware/toga: A Python native, OS native GUI toolkit.](https://github.com/beeware/toga)
  - [Toga 0.4.8](https://toga.readthedocs.io/en/stable/)

### Pyto
- [GitHub - ColdGrub1384/Pyto: Python IDE for iOS with NumPy, Matplotlib, Pandas, SciPy and SciKit-Learn](https://github.com/ColdGrub1384/Pyto)
  - [Pyto documentation — Pyto documentation](https://pyto.readthedocs.io/en/latest/index.html)

- Pyto 内のrubicon とtoga のバージョン
  - [GitHub - beeware/rubicon-objc at v0.4.2](https://github.com/beeware/rubicon-objc/tree/v0.4.2)
    - v0.4.2
  - [GitHub - beeware/toga at v0.3.0.dev29](https://github.com/beeware/toga/tree/v0.3.0.dev29)
    - v0.3.0.dev29


## Pyto のビルド

[GitHub - ColdGrub1384/Pyto at cd3b3de23fa22b5db9ddaea6b87b6c6fef3a4e69](https://github.com/ColdGrub1384/Pyto/tree/cd3b3de23fa22b5db9ddaea6b87b6c6fef3a4e69)

現在時点の最新をビルドしたが、Xcode でエラー吐く。
軽い気持ちでビルドしたので詳細確認までは未実施。


[Pyto/site-packages at cd3b3de23fa22b5db9ddaea6b87b6c6fef3a4e69 · ColdGrub1384/Pyto · GitHub](https://github.com/ColdGrub1384/Pyto/tree/cd3b3de23fa22b5db9ddaea6b87b6c6fef3a4e69/site-packages)

`./site-packages` に、モリモリとモジュールは入ったので、検証確認が必要そうなものたちをごっそりと持っていく
