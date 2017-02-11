---
layout: post
title: "기본 웹팩 세팅"
description: "간단하고 심플하게 빠르게 빌드하는 웹팩 세팅"
date: 2017-02-11
tags: [웹팩, webpack, build, bundler]
comments: true
share: true
---

![Webpack](http://jijong.github.io/images/img_webpack.png)

## webpack 간단하고 빠르게 웹팩을 적용해보기

***

튜토리얼을 바탕으로 그냥 내 입맛대로 필요할 것같은 모듈로 짠 소스 이다. 튜토리얼에서 나왔던 내용은 생략하고 간단명료하게 포스트 한다.

그럼 바로 소스로 넘어가서..

## webpack.config.js

```javascript

var path = require('path'),
    webpack = require('webpack'),
    HtmlWebpackPlugin = require('html-webpack-plugin'),
    ExtractTextPlugin = require('extract-text-webpack-plugin'),
    CopyWebpackPlugin = require('copy-webpack-plugin');

module.exports = {
    devtool: 'cheap-eval-source-map',
    entry: './src/js/common.js',

    output: {
        path: path.join(__dirname, './dist'),
        filename: './js/bundle.js'
    },

    module: {
        loaders: [
            {
                test: /\.css$/,
                exclude: /node_modules/,
                loader: ExtractTextPlugin.extract('style-loader', 'css-loader')
            }
        ]
    },

    plugins: [
        new webpack.optimize.UglifyJsPlugin({
            compressor: {
                warnings: false
            }
        }),

        new webpack.optimize.OccurrenceOrderPlugin(),

        new HtmlWebpackPlugin({
            template: './src/index.html'
        }),

        new ExtractTextPlugin('./css/bundle.css'),

        new webpack.ProvidePlugin({
            $: 'jquery',
            jQuery: 'jquery',
            'window.jQuery': 'jquery'
        }),

        new CopyWebpackPlugin([
            { from: './src/img/**', to: './img', flatten: true },
            { from: './src/css/fonts', to: './css/fonts', flatten: true }
        ])
    ]
};
```

## Plugin

* [html-webpack-plugin](#)
* [extract-text-webpack-plugin](#)
* [webpack.ProvidePlugin](#)
* [copy-webpack-plugin](#)

> 웹팩 내장 플러그인을 제외한 플러그인은 npm install 을 통해 설치한다.

### html-webpack-plugin

`template` 에 저장되어 있는 `src/index.html` 을 배포 폴더로 복사한다.

### extract-text-webpack-plugin

빌드한 `css` 파일을 `<head></head>` 태그안에 삽입되어 불러온다.

### webpack.ProvidePlugin

모듈을 자동으로 로드한다. 모듈에서 임의의 변수로 식별될 때마다 모듈이 자동으로 로드되며, 이 모듈은 로드된 모듈의 내보내기 모듈로 채워진다.

```javascript

new webpack.ProvidePlugin({
    $: 'jquery', // jquery 모듈을 불러온다.
    jQuery: 'jquery', // jquery 모듈을 불러온다.
    'window.jQuery': 'jquery' // angular.js 에서 jquery 를 사용시
}),
```

### copy-webpack-plugin

개별 파일 또는 전체 디렉토리를 빌드 디렉터리에 복사한다.

`{ from: 'source', to: 'dest' }` 이 기본적인 구조이다.

## 끝으로

아직 `webpack` 을 학습 중이지만 최신 프론트엔드 기술에는 없어서는 안될 필수적인 존재라고 느껴질 만큼 그 기능이 강력한것 같다.
 `babel` 을통한 `ES5` 빌드는 다음 포스트에 추가하겠다. `SASS` 빌드는 `webstorm` 의 자동 빌드 기능으로 생략하였다.

## 참고 사이트

* [copy-webpack-plugin 속성](https://www.npmjs.com/package/copy-webpack-plugin-hash)
* [웹팩 가이드](https://webpack.js.org/)
* [웹팩 튜토리얼](https://jijong.github.io/2016-12-02/webpack/)

