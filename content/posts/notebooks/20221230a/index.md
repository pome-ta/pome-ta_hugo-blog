---
title: "Docker 導入と使い方"
date: 2022-12-30
categories: ["notebook"]
tags: ["docker"]
menu: main
---

# Docker ことはじめ

久々にDocker を使うとなると、いろいろ忘れているので、メモをとりながら思い出す。

有料化とかの前に使っていて、再開するときに他のを調べてみたけど、結局面倒だったのでDocker を継続することにした。

## インストール

brew で入れる

```terminal
brew install --cask docker
```

Docker Desktop for Mac なので、`--cask` より

[docker — Homebrew Formulae](https://formulae.brew.sh/formula/docker#default) これではない。

インスコは結構時間かかる

### バージョン

```terminal
% >docker --version 
Docker version 20.10.21, build baeda1f

```

## チュートリアル

[概要説明とセットアップ — Docker-docs-ja 20.10 ドキュメント](https://docs.docker.jp/get-started/index.html)

docker は起動させておく

ちょっと面倒だったから、過去の自分のリポジトリを探す

### リポジトリリンク

基本的にN高 の無料期間の時のやつ

- Node
  - [pome-ta/intro-curriculum-3009: 入門コースの3章10節の練習 (ISC License)](https://github.com/pome-ta/intro-curriculum-3009)
  - [pome-ta/intro-curriculum-3007: 入門コースの3章7節の練習 (ISC License)](https://github.com/pome-ta/intro-curriculum-3007)
  - [pome-ta/nodejs-study](https://github.com/pome-ta/nodejs-study)

### とりあえず、テスト用にubuntu 入れたい

`Dockerfile` と、`docker-compose.yaml` の違いがわからんくなってきたので、とりあえずubuntu 入れて何かしたい。

### 結局チュートリアルやる

だめだ、いろいろ調べて分からなくなってきたから、公式チュートリアルやる

[Docker ドキュメント日本語化プロジェクト — Docker-docs-ja 20.10 ドキュメント](https://docs.docker.jp/index.html)

#### コンテナを見渡す

[Containers(コンテナ) を見渡す — Docker-docs-ja 20.10 ドキュメント](https://docs.docker.jp/desktop/use-desktop/container.html)

`Open in Visual Studio Code` コンテナの上にマウスカーソル移動しても、出てこない？🤔

#### サンプルアプリケーション

[サンプル・アプリケーション — Docker-docs-ja 20.10 ドキュメント](https://docs.docker.jp/get-started/02_our_app.html)

`package.json` と同フォルダに`Dockerfile` を作っていて、`/app` ディレクトリ内で、

```terminal
docker build -t getting-started .
```

これしてもこけるよね？

vscode でなくて、terminal でやると、通った。多分、vscode のpath の取り回しとか違う？

`/app` でやる。root ではないことを気を付ける。とりあえず走った。
