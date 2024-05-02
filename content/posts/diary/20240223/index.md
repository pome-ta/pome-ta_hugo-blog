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
