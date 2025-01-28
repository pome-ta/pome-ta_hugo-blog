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


## カジュアルな考え

- Pythonista3 では、
  - VieeController(NavigationController) を実装
  - App 自体の`rootViewController` を取得
  - MainThred 上で
    - 取得したController から`.presentViewController` で実装Controller を差し込む
  -  `.dismissViewControllerAnimated_` で閉じる
    - `visibleViewController = self.visibleViewController` と、ViewController 呼んでる
    - `self.` で、NavgationController 自体を閉じてもいいかも？

(Pyto は一旦置いておいて)a-shell だと、なにかしらのViewController の`.viewDidDisappear_` で落ちる

また、落ちない場合もあり、再現性として不明。


### まずまず

- Pyto で、toga とrubicon-objc が使われている
- toga のlifecycle の挙動に倣いたい
  - toga のオブジェクトとして、rubicon をwrap している
- Pyto も、自身のViewController から生やしている様子

という感じなので、toga オブジェクトとなっているところをrubicon のオブジェクトにまで剥がし、a-shell で実行できるようにしたい


だけども、現在Pythonista3 とa-shell でasyncio するときに、`loop.run_forever(lifecycle=iOSLifecycle())` としておらず、`loop = asyncio.new_event_loop()` で走っちゃってるのよな。。。


Pyto でも、`loop.run_forever(lifecycle=iOSLifecycle())` で動かしているみたいなのよね・・・






