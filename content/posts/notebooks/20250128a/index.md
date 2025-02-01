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
    - 取得したController から`.presentViewController_` で実装Controller を差し込む
  -  `.dismissViewControllerAnimated_` で閉じる
    - `visibleViewController = self.visibleViewController` と、ViewController 呼んでる
    - `self.` で、NavgationController 自体を閉じてもいいかも？

(Pyto は一旦置いておいて)a-shell だと、なにかしらのViewController の`.viewDidDisappear_` で落ちる

また、落ちない場合もあり、再現性として不明。


### まずまず、つらつらと。。。

#### 参照先実装の要件を剥がしていきたい

- Pyto で、toga とrubicon-objc が使われている
- toga のlifecycle の挙動に倣いたい
  - toga のオブジェクトとして、rubicon をwrap している
- Pyto も、自身のViewController から生やしている様子

という感じなので、toga オブジェクトとなっているところをrubicon のオブジェクトにまで剥がし、a-shell で実行できるようにしたい


だけども、現在Pythonista3 とa-shell でasyncio するときに、`loop.run_forever(lifecycle=iOSLifecycle())` としておらず、`loop = asyncio.new_event_loop()` で走っちゃってるのよな。。。


Pyto でも、`loop.run_forever(lifecycle=iOSLifecycle())` で動かしているみたいなのよね・・・


#### App 上でPython が走るということは、どうゆうことや？

Pyto やa-shell のPython 実行の動きを確認しなきゃなんとも言えないけども、App 自体のViewController から差し込んでおるので、閉じたら閉じて欲しい。
とはいえ、`.presentViewController_` は、MainThred 上でないと、落ちるからその辺をケアしたい。


思いつきで、[UISheetPresentationController | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uisheetpresentationcontroller?language=objc) で表示させたりしてみるけど、結局のところ独自View を表示させるためにワンクッション入れているだけな印象なので、意味はないかも。



#### life cycle とは？

toga では、iOS のlifecycle はずっとぶん回す(という雑な理解) かたちでの実装をしているが、Pythonista3 で`eventloop.py` を呼び出すときには、`iOSLifecycle` を使わないと実行ができる。

toga は、無の状態(と、表現をしていいのか？) からのスタートだから、そういった仕様としている？でもPyto も同じ？(いや、オーバーライド時に上書きして消してる？)


### Pyto のコードで気になる部分追っかけ


- [pyto_ui.py #L8039](https://github.com/pome-ta/pystaRubiconObjcSandBox/blob/1571e7898b69459fdc0538cfaaf6dcd9efe372aa/sandbox/pytoTest/intoPytoModules/Lib/pyto_ui.py#L8039) `def show_view_controller(view_controller: "UIViewController"):`
  - [#Using UIViewController | pyto_ui — Pyto documentation](https://pyto.readthedocs.io/en/latest/library/pyto_ui.html#using-uiviewcontroller)



#### Semaphore

- [Pyto/Pyto/Model/Python Bridging/PyMainThread.swift at main · pome-ta/Pyto · GitHub](https://github.com/pome-ta/Pyto/blob/main/Pyto/Model/Python%20Bridging/PyMainThread.swift)
  - `let semaphore = Python.Semaphore(value: 0)` ってところ
- [Semaphoreを使ってPythonの非同期処理の平行処理数をコントロールする](https://zenn.dev/yosemat/articles/39c36d0ed88a7c)
- [【Swift】@escaping属性のクロージャとは #Xcode - Qiita](https://qiita.com/imchino/items/48564b0c23a64f539060)

#### Python を埋め込む

- [iOSのSwift,Objective-CでPythonを呼び出す #Python - Qiita](https://qiita.com/Hiroki_Kawakami/items/830baa5adcce5e483764)
- [1. 他のアプリケーションへの Python の埋め込み — Python 3.10.16 ドキュメント](https://docs.python.org/ja/3.10/extending/embedding.html)




## 次回

> [`rubicon-objc` と`a-Shall` と - pome-ta_hugo-blog](https://pome-ta.github.io/pome-ta_hugo-blog/posts/notebooks/20250201a/)

なんとなくの解決編


