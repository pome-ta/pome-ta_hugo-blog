---
title: '`rubicon-objc` と`a-Shall` と'
date: 2025-02-01
categories: ['notebook']
tags: ['Python', 'rubicon-objc', 'a-Shall']
menu: main
draft: false
---

# Pythonista3 のobjc を使ったUIKit 挙動をa-Shell で動かしたい


> [`rubicon-objc` と`toga` と `Pyto` と - pome-ta_hugo-blog](https://pome-ta.github.io/pome-ta_hugo-blog/posts/notebooks/20250128a/)

続きというか、続報というか

- [a-Shell](https://holzschu.github.io/a-Shell_iOS/)
- [GitHub - holzschu/a-shell: A terminal for iOS, with multiple windows](https://github.com/holzschu/a-shell)
- [About the book | A guide to a-Shell](https://bianshen00009.gitbook.io/a-guide-to-a-shell)

a-Shell で実行ができればオールOK案件。

なぜならば、a-Shell はfree のApp だから。誰かが気軽に試そうとした場合、有料App のPythonista3 やPyto ではハードルが高い。

- Pythonista3 はApp のソースコードなし
- Pyto はGitHub にコードあり
  - 内部で、rubicon とtoga を使っている
- (a-Shell は、[ios_system(GitHub - holzschu/ios_system: Drop-in replacement for system() in iOS programs)](https://github.com/holzschu/ios_system/) が私には、ドデカすぎて一旦パス)

として、toga とPyto を調べ始めた


## toga とPyto

- toga
  - (ことiOS に焦点を絞ると)
  - iOS の挙動は、Pyto やPythonista3 と違い、自身を起点として完了までをライフサイクルが見守るかたち
    - コードを見た感想としてそんな感じ。実際に動かせてはいない
  - モバイルApp のPython から実行をする。という実装は現在のところ想定していない感じ

- Pyto
  - 大まかには、Rubicon を使って実装をしている
    - が、さまざまにwrap している状態な印象、手厚く状態管理をしているのかな？と
    - toga の実装を使いつつ、ほぼほぼtoga としての機能の上澄部分を取り出し、Pyto 用にリアレンジしている印象
  - つまるところ、Pythonista3 の実行の流とほぼ同じでは？
    - 「参考になるところ」というか、コードを追いかけつつ「あーここで、○○しているのかー」という確認ができた



実装方法や手法に関しては、難しかったけど勉強して、理解した（ふり）ができたので有意義ではあった


## asyncio 処理


eventloop のモジュールは使った

iOS のは使わずに、デフォルトのようなやつで実行

UIKit が稼働中は、loop 内として、終了時にloop にストップをかけるかたち

