---
title: "macOS をクリーンインスコする事前メモ"
date: 2024-02-23
categories: ["diary", "macOS" ]
tags: ["memo", " dotfile", "macOS", "upgrade", "update"]
menu: main
draft: false
---

# macOS をアプデするぞ

- アプデの前の事前整理をしたい
  - dotfile
  - ローカルにあるものの移動
    - GitHub にup できるのであればやる
  - 何を残して何を捨てていいのか
    - 一括でできるものはできるように
  - anyenv のままにするか、asdf ってどうなんやろ？
    - 発端としては、deno がanyenv に対応してないっぽいから
      - deno ってそうゆうことやるのか？
      - そもそもdeno やる？
    - docker で完結してしまう？
      - 多分重くなっちゃったり、気軽にプロジェクトを触るってことができなくなる？
  - `zsh` ? `bash` ?
    - なんか、色々といい加減にしてきたから統一できてもいいかもね
- とりま、全部1からするか！とりあえず逃すものをまとめたい
  - なにかしらデスクトップにあったものは退避した

```.terminal
% >brew list
==> Formulae
anyenv  git  lz4  python@3.10 vim
aria2  git-lfs  mpdecimal python@3.11 xz
berkeley-db libiconv ncurses  python@3.12 zlib
berkeley-db@5 libsodium openssl@1.1 python@3.9 zsh
bzip2  libssh2  openssl@3 readline zstd
ca-certificates libyaml  pcre  ruby
gdbm  libzip  pcre2  sqlite
gettext  lua  perl  tree

==> Casks
algodoo   github   sf-symbols
audacity  google-chrome  steam
blender   inkscape  vimr
docker   jetbrains-toolbox visual-studio-code
epic-games  min   vivaldi
firefox   minecraft  xcodes
font-jetbrains-mono obsidian  zoom
gimp   runjs

```

## ただいま！

とりまここまで最低限の設定は完了かも？

毎回忘れるからメモをしていきたい。ので、雑多に列記していく

- ゴリっと全部消す
  - インストール関係が結構時間かかった
  - 「ようこそ」の直前のりんごアイコンが、通常は白のはずなのに、緑→黄色になってた
    - グラフィック関係でなにかごちゃっとしているのかしら？
- 最低限の準備をする
  - HomeBrew
    - xcode のコマンドラインを一緒にDL して時間かかった
    - もしかしたら、先にxcode 入れてもよかったかも？
      - なんだかんだでxcode 使うし（使いたいし）
  - xcode
    - 毎度時間かかるから、放置
  - zsh
    - 初期からzsh だけど、アプデの意味で
  - anyenv
    - asdf（？） と悩んだけど、とりまでanyenv
      - deno の管理できたらいいなぁと思っていて（使わないのに）
    - 初期設定
      - 手動でやるところあり
    - nodenv
      - `22.0.0` と最新とした
      - 結構はやかった
        - 正しくまだ使ってないけど、なんかあるかな？
    - pyenv
      - `3.10.14` とした
        - Pythonista3　と揃えたい気分として
      - anyenv からのpyenv でのエラーがあったので、無事に踏んだ
        - Twitter にあげてるから、後から入れる
    - vim
      - なんか、初期も`9.` のあたらしめだったけど、アプデの意味で
      - なんとなく、言語関係を事前に入れてからー。と考えていたけども、Python が`3.12` とか入れてた気がした
        - 他にもPerl やらなんやら、入れてたから、あまり気にしなくてもよかったかも
    - git
      - Github のSSH も含めて
      - 大体、公式案内通り
        - 最後の`Sudo` コマンドでの確認！みたいなのが、実際のコマンドが出てなかったからググった
        - 初回接続の「マジでいいの？」的な英語が読み解けず、`config` を書いたり消したり。。。
      - そんなこんなで、Git 自身の`config` も`--global` で入れている
    - font
      - cask にもないじゃん！と思ったら、tap 使ってfont 管理するみたい
      - 完全に忘れていたのでよかった
      - nerd フォント気になる
    - vscode
      - vim コマンドにするか。。。

### `.rc` 系

拘らないようにしようと思いつつ、色々と手を加えていきそう。。。

terminal もちょっとばかし変更をしていこうかなぁと、、、nerd font もきになるし

### 手動のOS 設定

キーボードの`fn` でのやつや、トラックパッドの3本指など、設定が点在している印象でモヤモヤ
点在というか、深くなりすぎ？項目になかなかピンと来ず、ググれば出てきたのでよかったけど

さて、さっきはGitHub Desktop でpush 成功したが、git コマンドでpush できるかな？（これが読めてたらできてる）
:w

      
