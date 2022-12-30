---
title: "Style の調整"
date: 2022-12-30
categories: ["hugo"]
tags: ["hugo", "sample", "style", "css"]
menu: main
---


# 表示フォントの調整

```custom.css
/* @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@100;300&display=swap');
body {
    font-family: 'Noto Sans JP', sans-serif;
} */

body {
  font-family: 'Helvetica Neue', Arial, 'Hiragino Kaku Gothic ProN',
    'Hiragino Sans', Meiryo, sans-serif;
  font-feature-settings: 'pwid' 1;
}

.logo__text {
  text-transform: none;
}

```

`Noto` から、よくあるやつにしてみている

## 参照先

### `font-family` 設定

[2022年に最適なfont-familyの書き方 - ICS MEDIA](https://ics.media/entry/200317/)

毎年確認するのが楽しみなやーつ

### `feature-settings` 設定

取り急ぎで。少々詰まってる感出るかも。
