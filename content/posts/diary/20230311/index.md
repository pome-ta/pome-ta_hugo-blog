---
title: "あれやこれやと、書き落としていく所存でありたい"
date: 2023-03-11
categories: ["diary", "output" ]
tags: ["JavaScript", " spreadsheet", "GLSL", "shader", "sound", "codemirror"]
menu: main
draft: false
---

# メモ魔にでもなりたい所存

iPhone でStable Diffusion の実装実験をやっていたけども

なんだか無理そうだし、ストレージが逼迫してしまうので、しれっとフェードアウト。

GLSL でのランダムやノイズの検証のために、Python 上で確認したいモチベーションから

`uint8` やら`float32` やらの部分と悪戦苦闘しながら、

処理速度の関係から、Numpy へお引越し。Numpy は基本的に触っていなかったので

関数や文法・お作法の基本的なところからお勉強。

結局のところ、ランダムとしてのhash シフトやら、数学的な理解よりも

Numpy 実装の方に集中してしまう。

発作的に発生する、パーリンノイズまではなんとかいく事ができ、一瞬トーンダウンしたので

GLSL のサウンドシェーダーへと、河岸を変えることに。

## 自分の過去の実装が理解できない

サウンドシェーダーに関しては、過去にシェーダーエディタとしてcodemirror を使ったリアルタイムエディタがある。

リアルタイム処理をするエディターって便利かも。と思っていたが

実際使おうとすると、内部処理が走っていると思ってしまうのか、そわそわしてしまって、なかなか集中ができない。

時々、使うくらいで携帯上ではPythonista3 のエディタで記述し、実行結果を確認する程度になっている。

PC 上だと、案外使うことがありえるのであるが、どうもファンがブン回ってしまう。

参照先である、twigl は、レンダーを止める設定にすると、唸り上がることはないから、私の内部実装が悪いようである。

codemirror も、全然理解しないまま実装をしていたが、結構日が経っていたので、気合いでアプデ

`node_modules` と、`package-lock.json` を削除し

```terminal
npm i
```

をする男気あるアプデを実行した。現在の観測上だと、問題なく動いているっぽい。

そして、キモの部分のサウンドシェーダーの部分が、読み返してもふんわりなのである。

参照元のtwigl との相違点も、なぜそのようにしたのか、記憶が曖昧で

今後、揃えた方がいいのかそのままでいいのかも、検証のために時間を作ることになりそうである。

## メモなー

Numpy のGLSL 模擬実装に関しても、現在はギリで記憶にあるが今後何かの拍子で使おうとしても、テキストが残っていないのである。

使おうとする場面がある意味恐怖でもありそうだけど

ともかく、メモやらなにやら、アウトプットを意識して、参照できるようにすれば

記憶するという行為が不要になるので、やっていきたいなぁと思うのである。

codemirror のアプデであっても、そもそもnpm コマンドを忘れていたり、ビルド手順など

調べ直して、そして同じ参考記事を読む無駄な時間なのである。

### メモしておきたいこと

現在、なんとなくメモしなきゃリストとしては

- GLSL 風なNumpy の書き方
- node やnpm のふわりと疑問に思っているものと、その対策や理解
- Codemirror の現状理解できていることと、理解したいこと
  - どんな理解のしかたをすればいいかとか
- WebGL 実装の整理
  - デバッグ方法を調べて、スタンダードを知る

趣味のこと以外でも、仕事で黒魔術的に使っているspreadsheet もまとめられれば

- 最近の`LET` やら`LAMBDA` と`MAP` の理解
  - 配列処理と、プログラミング的な処理との違い
  - 関数型言語理解にも繋がるかしら？

的な