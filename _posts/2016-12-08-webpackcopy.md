---
layout: post
title: "웹팩으로 개발파일, 빌드파일 분류하기"
description: "웹팩으로 개발파일, 빌드파일 복사하는 얕은 지식"
date: 2016-12-08
tags: [웹팩, webpack]
comments: true
share: true
---

## copy-webpack-plugin


HTML 파일을 빌드하는 html-webpack-plugin 말고 html파일 이외에 다른 파일들을 옮길 수 있는 모듈이 있다.

```js
$ npm install -d copy-webpack-plugin
```

## webpack.config.js


```js
var CopyWebpackPlugin = require('copy-webpack-plugin');

module.exports = {
  plugin: [
    new CopyWebpackPlugin([
        { from: './src/img/**', to: './img/', flatten: true }
    ])
  ]
};
```
`html-webpack-plugin`처럼 `webpack.config.js`에서 플러그인 모듈을 추가한다. `from`은 개발파일 `to`는 빌드파일 경로로 설정하면 되고, `flatten: true` 값을 주어 복사되는 파일이름만 저장되게 한다.

Terminal창에 `webpack` 을 실행하여 번들링을 하게되면 정상적으로 빌드파일 경로에 파일들이 삽입된다.
