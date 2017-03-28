---
layout: post
title: "웹팩에서 file-loader로 이미지 불러오기"
description: "웹팩에서 이미지 경로 설정 및 불러오기"
date: 2017-03-28
tags: [study, js, 웹팩, webpack]
comments: true
share: true
---

![file_loader](http://jijong.github.io/images/img_fileloader.svg)

# Webpack에서 file-loader로 이미지 불러오기

***

ES6 학습하기전 웹팩을 학습하면서 `css-loader` 및 `ExtractTextPlugin` 플러그인을 사용해
로드하고 번들링을 한다. 그리고, 이미지 등 다른 확장자를 가진 파일들은 `file-loader`를 통하여 로드 할 수있다. 
예제는 [npm](https://www.npmjs.com/package/file-loader)에 잘나와있지만 보기쉽게 정리 할겸 포스팅 하였다. 
참고로 개발환경은 웹팩1에서 작업하였다.

### 목차

* [설치](#설치)
* [사용법](#사용법)
* [webpack.config.js Examples](#webpack.config.js-Examples)
* [예시](#예시)
* [참고 링크](#참고-링크)

### 설치

```javascript
npm install -i -d file-loader
```

개발모드로 `file-loader` 모듈을 설치한다.


### 사용법

```javascript
use: "file-loader?name=[name].[ext]&publicPath=assets/foo/&outputPath=app/images/"
```

- [ext] 파일의 확장자
- [name] 파일의 이름
- [path] 파일의 기본 경로를 지정한다.
- [hash] 기본적으로 생략된 내용의 해시 태그를 사용한다.
- [<hashType>:hash:<digestType>:<length>] 이것들중 선택 할 수 있다.<br />
    other hashTypes, i. e. sha1, md5, sha256, sha512<br />
    other digestTypes, i. e. hex, base26, base32, base36, base49, base52, base58, base62, base64
    and length the length in chars
- [N] 파일 이름과 일치하지 않는 파일 이름을 param으로 전송하여 파일을 일치 시킨다.


### webpack.config.js Examples

```javascript
...

module: {
        loaders: [ // 어플리케이션을 위해 적어줄 로더들 배열
            {
                test: /\.(jpe?g|png|gif|svg)$/i, // 이미지 로더
                exclude: /node_modules/,
                loader: 'file-loader?name=[name].[ext]&publicPath=../images/&outputPath=./images/' // PublicPath : css 이미지 폴더 경로, outputPath : 이미지 폴더 경로
            }
        ]
    }
```

당신은 `publicPath` 지시어를 통하여 불러오는 파일의 기본 폴더 위치를 지정할 수 있고, `outputPath` 지시어를 통하여
업로드 하는 파일의 경로를 지정해 줄 수 있다.

### 예시

```javascript
require("file-loader?name=js/[hash].script.[ext]!./javascript.js");
// => js/0dcbbaa701328a3c262cfd45869e351f.script.js 
 
require("file-loader?name=html-[hash:6].html!./page.html");
// => html-109fa8.html 
 
require("file-loader?name=[hash]!./flash.txt");
// => c31e9820c001c9c4a86bce33ce43b679 
 
require("file-loader?name=[sha512:hash:base64:7].[ext]!./image.png");
// => gdyb21L.png 
// use sha512 hash instead of md5 and with only 7 chars of base64 
 
require("file-loader?name=img-[sha512:hash:base64:7].[ext]!./image.jpg");
// => img-VqzT5ZC.jpg 
// use custom name, sha512 hash instead of md5 and with only 7 chars of base64 
 
require("file-loader?name=picture.png!./myself.png");
// => picture.png 
 
require("file-loader?name=[path][name].[ext]?[hash]!./dir/file.png")
// => dir/file.png?e43b20c069c4a01867c31e98cbce33c9 
```

### 참고 링크

- [file-loader](https://www.npmjs.com/package/file-loader)
- [npm](https://www.npmjs.com/)
