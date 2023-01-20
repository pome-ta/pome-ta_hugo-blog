---
title: "Pythonista3 でStable Diffusion を動かせるように挑戦しているはなし"
date: 2023-01-20
categories: ["diary", "Pythonista3" ]
tags: ["Python", "Markdown"]
menu: main
---

# Stable Diffusion 動くかな？

ここらへんを参考にしている。

[iOSとMacOSに🤖機械学習🤖を用いたテキスト入力に基づく描画を実現（Stable Diffusion + Core ML） - Qiita](https://qiita.com/MaShunzhe/items/63950679bf54b966ffc4)

[【Swift】iOSでStableDiffusionを使ってみた - Qiita](https://qiita.com/SNQ-2001/items/2d33dc535cf106189f75)

まずは、mac でXcode で動くか確認。

エミュレーターだと超時間かかって、画像出力したけど、iPhone （11） に繋いで実行したら、時間かかって落ちた。

## たぶん、アプリの制約的にメモリで落ちるのではないかと思っているの

Xcode での正規上では、とりあえず動いたので、Pythonista3 で挑戦をする。

[apple/ml-stable-diffusion: Stable Diffusion with Core ML on Apple Silicon](https://github.com/apple/ml-stable-diffusion)

これを、Pythonista3 (Python) に書き換える。リポジトリ上のPython コードではなく、Swift のコード。

Python のコードは、必要なライブラリが多くて、Pythonista3には使えないので、`objc_util` で、Swift コードをObjective-C に読み替えたりして、実装する。

現在、基本的なロードは完了し、トークンを分割したりくっつけたりしている。

まじで、分割してくっつけている、作業工程が意味不明。流れが理解できていないけど、処理の通りに進めている状態。

Swift 独自のお作法を知らないので、シコシコ調べつつの移植。スクリプト言語メインの私だと、理解の範疇を超えることが多くありますね。

### ストレージが逼迫されている

とりあえず実行。みたいなことをもちろんやるのだけど。Pythonista3 の容量が12GB とかなっていて驚いた。

読み込みから、解放ができていないのかしら？

とりあえず、Pythonista3 のアップデート案内も来ていたので、気軽にアンインストールしても運用できるように、サクッと削除して再度環境を整えた。

一回実行するたびに、150MB とか増えていくんですが。。。
