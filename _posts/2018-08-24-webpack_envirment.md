---
layout: post
title: "Webpack으로 개발환경 구축하기"
description: "Webpack으로 자동화 프론트엔드 개발환경 구축하기"
date: 2018-08-24
tags: [study, 웹팩, webpack, build, bundler, front-end]
comments: true
share: true
---

# Webpack을 활용한 개발환경 구축

***

너무 오랜만에 포스팅 한다. 그만큼 공부를 게을리 했던것.. 다시 열심히 해야겠다.
이 포스트는 회사에서 아이디어 공유시간에 만들었던 발표자료를 내 개인블로그에 포스팅 하였다.
개발환경 구축할때 참고하면 되겠다.  :) 

## 목차

* [IDE 선택](#ide-선택)
* [Node.js & NPM](#nodejs--npm)
* [ES6 & Babel](#es6--babel)
* [SASS](#sass)
* [Webpack](#webpack)
* [Q&A](#qa)
* [참고 링크](#참고-링크)

## IDE 선택

<img src="https://github.com//qnfzks55/webpack_lmj/blob/master/webstorm.png?raw=true" />

### 웹스톰 (Webstorm)

1. `HTML,CSS,JS` 프론트엔드에 최적화된 IDE
2. 지속적인 업데이트로 `es6` 및 `react`, `Vue.js` 까지 대세 언어 지원
3. 코드 검사 및 탐색, 리팩토링 지원
4. `Node.js` 지원
5. 강력한 `VCS` 지원
6. `Emmet` 및 젠코딩 지원으로 빠른 코딩 가능
7. 다양한 확장자의 `watcher` 지원 (`sass` 같은 경우는 `ruby` 설치 후 `gem` 인스톨 설치)

> 이외에도 워낙 좋고 빠른 IDE가 잘출시되어있으므로,<br />각 IDE의 장단점들이 있으므로 개인이 판단하여 취향껏 입맛대로 골라 쓰면 될듯함.

## Node.js & NPM

<img src="https://github.com//qnfzks55/webpack_lmj/blob/master/npm_node.jpg?raw=true" />

### Node.js
1. 자바스크립트 문법으로 웹서버나 smtp 서버 등과 같은 서버 프로그램을 작성할 수 있게 하는 서버 사이드 자바스크립트 언어.
2. `Express.js` 프레임워크를 사용하면 번거로운 작업들을 해결해주어 빠르게 웹서버를 구축할 수 있다.
3. 그러나 클라이언트 & 서버개념 등 웹의 구조 학습이 필요하다.

### NPM
1. Node.js 기반 패키지 모듈들을 관리하는 도구.
2. 작은 모듈들을 필요함에 따라 설치하여 개발자에게 편리함을 제공한다.
3. `Terminal` 에서 명령어를 입력하여 실행한다.
4. `package.json` 을 설치하여 이 파일로 모듈들을 관리한다.

### 명령어

#### 1) 설치
`npm install` (모듈 설치)<br />
`npm install --save-dev package` (개발모듈로 패키지 설치)<br />
`npm install --save package` (배포모듈로 패키지 설치)<br />
`npm install --g package` (global로 패키지설치)
#### 2) 제거
`npm uninstall package`
#### 3) package.json 생성
`npm init`<br />
`npm init y` (옵션 설정없이 바로 package.json을 생성해주는 명령어)

### Package.json
```javascript
{
    "name": "name",
    "version": "1.0.0",
    "description": "설명",
    "main": "webpack.config.js",
    "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    },
    "author": "Author",
    "license": "ISC",
    "devDependencies": {
    "babel-core": "^6.26.3",
    "babel-loader": "^7.1.5",
    "babel-preset-env": "^1.7.0",
    "babel-preset-es2015": "^6.24.1",
    "babel-preset-react": "^6.24.1",
    "babel-preset-stage-2": "^6.24.1",
    },
    "dependencies": {
    "webpack": "^4.16.1"
    }
}
```
1. Npm을 통하여 설치한 의존성 모듈들의 버전 관리와 프로젝트에 대한 관리를 하는 파일.
2. `Terminal` 에서 `npm init` 명령어를 통하여 생성
3. `script` 에서 `run` 명령어를 설정해주어 실행할 모듈을 설정해줄수 있다.
4. 의존성모듈들은 `dependencied` 모듈에, 개발의존성모듈들은 `devDependencies` 모듈로 설치하여준다.

## ES6 & Babel

<img src="https://github.com//qnfzks55/webpack_lmj/blob/master/babel.jpg?raw=true" />

1. `Typescript`, `CoffeSCript`, `ES6` 등 기존 `Javascript` 문법이 아닌 각각의 문법으로 코딩된 소스를 `Javascript` 문법으로
`transcompile` 해주는 모던 웹기술에서 필수적인 모듈이다.
2. `babel` 7버전 부터 모든 `babel package` 들이 `@babel` 이라는 `Namespace` 안에 속하게 되었다.

> 예시 : npm i -D @babel/cli @babel/core @babel/preset-2015

### 사용법

#### 1) 전역으로 `babel` 을 설치한다.
`$ npm i -g babel-cli`
#### 2) 개발 의존성모듈로 `babel-cli`, `babel-preset-2015` 모듈 설치
`$ npm i –D babel-cli babel-preset-2015`
#### 3) `.babelrc` 파일을 생성한다.
```javascript
{
  "presets" : ["es2015"]
}
```
#### 4) 폴더 구조
```
| es6/
|   |- script.js
|- .babelrc
|- index.html
|- package.json
```

#### 5) es6/script.js
```javascript
const test = 5;
const clickEvent = () => console.log(test);
```
#### 6) `Terminal` 에서 `babel` 명령어로 `transpiling` 해준다.
`$ babel es6/script.js –d script -w`
#### 7) 트랜스파일된 script.js 파일을 확인해보면
```javascript
var test = 5;
var clickEvent = function clickEvent() {
    return console.log(test);
};
```

## SASS

<img src="https://github.com//qnfzks55/webpack_lmj/blob/master/sass.png?raw=true" width="400" />

문서의 구조를 깔끔하고 구조적으로 기술하는 데 사용하는 기술인 `css`의 상위에 있는 메타언어로, `Javascript` 처럼 특정 속성의 값을 변수로 선언하여 필요한 곳에 선언된 변수를 적용할 수도 있고, 반복되는 코드를 한 번의 선언으로 여러 곳에서 재사용할 수 있도록 도와주는 일종의 **CSS 전처리기**

### 설치
1. `Sass` 는 `Ruby` 라는 프로그래밍 언어를 기반으로 하므로 `Ruby` 를 설치한다.
2. `Sass` 를 설치한다.<br />
`$ gem install sass`

### Webstorm 에서 SASS 세팅
1. `settings` -> `Tools` -> `File Watchers` 에서 사용할 문법을 선택한다.
2. `SCSS` 를 선택했다 치고 `Program` 에서 `Ruby` 에서 `gem` 으로 설치한 `scss.bat` 파일을 경로로 잡아준다.

<img src="https://github.com//qnfzks55/webpack_lmj/blob/master/w_scss.jpg?raw=true" />

3. `Webpack` 에서 `SCSS` 를 `Javascript` 로 해석할 수 있게 `loader` 를 설치한다.<br />
`$ npm i -D node-sass css-loader style-loader sass-loader`

> * `style-loader`, `css-loader` : 보통 CSS를 번들링하기 위해서 쓰는 `loader` 세트이다.
> * `sass-loader` : `scss` 및 `sass` 를 해석할 수 있게 해주는 `loader` 이다.

```javascript
module: {
	rules: [ 
		{
			test: /\.(scss|sass)$/, 
			exclude: /node_modules/,
			use: ['style-loader', 'css-loader', 'sass-loader']
		},
	]
}
```

### SASS와 SCSS의 차이
* `Sass` (indented Syntax 들여쓰기 문법)
    * 이전 버전으로 `Sass` 확장자는 `Ruby`의 영향을 받은 간결한 문법을 사용한다.
    * `CSS` 문법에서 반복 사용되는 {}, ; 등을 사용하지 않는다.
    * 변수명에 ! 를, 속성과 값의 구분자인 특수기호로 = 를 사용한다.
* `SCSS` (`CSS`와 같은 문법)
    * SS3에 맞춰서 업데이트 버전으로 CSS Syntax와 비슷하면서 유연한 문법 등을 제공한다.
    * 변수명에 $를, 속성과 값의 구분자인 특수기호로 :(콜론)을 사용한다.  

## Webpack

<img src="https://github.com//qnfzks55/webpack_lmj/blob/master/w_map.png?raw=true" />

웹페이지를 구성하는 수많은 요소(html, js, css 파일 외에도, 웹폰트, 이미지, json 데이터 등)를 파일 하나로 압축하여
웹페이지의 `request` 를 줄일 수 있도록 도와주는 `Gulp`, `Grunt` 와같은 **모듈 번들러**

### 특징
1. 파일을 압축 및 난독화 해주고 크로스 브라우징도 대응해주어 굉장히 편리한점이 많다.
2. `Javascript` 가 클라이언트단 서버단 모두에서 대세가 된 만큼 수많은 의존관계가 생기면서 이것들을 하나의 파일로 압축 및 병합해주어
의존성 관리를 효과적으로 할수 있다.
3. 파일이 너무 많거나 용량이 클 경우, 개발자 마음대로 번들링할 파일 수를 정하여 자유롭게 설정을 할 수 있다.
4. 현재 `Webpack 4` 까지 릴리스 되었는데 `Webpack 1~3` 에서 추가 및 수정, 삭제를 보완하여 빠르게 업데이트를 해주고 있다.
5. 기본적으로 `ES6` 에서 추가된 모듈 시스템 개념(`import`, `require`, `export` 등)과 `Node.js`, `npm` 을 쓸 줄 알아야 한다.

### Webpack.config.js 세팅
`Webpack` 의 실행과 모든 기능이 담기는 기본적인 생성 파일이다.<br />
다른 이름으로 변경 시에는 `–config` 명령어를 통하여 실행해야 한다.

```javascript
const path = require('path');
const webpack = require('webpack');
const HtmlWebpackPlugin = require('html-webpack-plugin'); 
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
    mode: 'development', 
    entry: ['./src/js/app.js'], // 번들링 포인트
    output: { // 배포 파일
        /** 번들 파일 저장 폴더
         * __dirname : node에서 제공하는 node 파일의 경로를 담고 있는 특별한 변수
         * path.join('a', 'b')
         * path.join('a/', '/b')
         * path.join('a', '/b')
         * path.join('a/', 'b')
         * 등 / 에 상관없이 join() 메서드로 경로 오류를 잡아줌
         */
        path: path.join(__dirname, './dist'),
        filename: './js/bundle.js' 
    },
    module: {
        rules: [ // 어플리케이션을 위해 적어줄 로더들 배열
			{
				test: /\.scss$/, // 로더가 적용될 파일 매칭을 위한 배열
				exclude: /node_modules/,
				use: ['css-hot-loader', MiniCssExtractPlugin.loader, "css-loader", "sass-loader"]
			},
			{
				test: /\.html$/,
				exclude: /node_modules/,
				use: 'raw-loader'
			},
			{
				test: /\.js$/,
				exclude: /node_modules/,
				use: {
					loader: 'babel-loader',
					options: {
						babelrc: true,
						presets: ['es2015']
					}
				}
			},
			{
				test: /\.(jpe?g|png|gif|svg|ico)$/i,
				exclude: /node_modules/,
				use: 'file-loader?name=[name].[ext]&publicPath=../img/&outputPath=./img/'
			}
        ]
    },
	plugins: [
        new webpack.HotModuleReplacementPlugin(),
        new HtmlWebpackPlugin({
            template: './src/index.html'
        }),
	    new MiniCssExtractPlugin({
		    filename: "./css/common.css"
	    })
    ]
};
```
#### 1) mode
`Webpack 4` 에서 새로 추가된 옵션이다. `mode` 가 `development` 면 개발용, `production` 이면 배포용이다.<br /> 
배포용일 경우에는 알아서 최적화가 적용된다. `mode` 옵션의 추가로 개발용과 배포용으로 `webpack.config.js`를 나누기가 더욱 편리해졌다.

#### 2) entry
`Webpack` 의 번들링 엔트리 포인트다. 여러개의 번들파일을 생성하기를 원하면, 여러개의 엔트리 포인트들을 만들수도 있으며,
배열로도 나열할 수 있다.

```javascript
{
    entry: {
        app: '파일 경로',
        main: '파일 경로',
    }
}
```

위와 같이 하면 `app.js`, `main.js` 두 개가 생성된다. 결과물로 여러 `js`를 만들고 싶을 때 저렇게 구분해주면 된다.

```javascript
{
    entry: {
        app: ['one.js', 'two.js', 'three.js']
    },
}
```

앞에서 설명했듯 위의 배열의 경우는 `one.js` 랑 `two.js`, `three.js` 가 한 파일로 엮여 `app.js` 로 합쳐진다. 이렇게 웹팩은 `entry` 의 `js` 파일부터 시작해서 `import, require` 관계로 묶여진 다른 `js` 까지 알아서 파악한 뒤 모두 `entry` 에 기재된 **키 개수** 만큼으로 묶어준다.

#### 3) output
`Webpack` 에 의해 출력되는 형태를 나타낸다.

```javascript
output: { // 배포 파일
    publicPath: '/',
    path: './dist',
    filename: './js/[name].js' 
}
```

> path - 번들된 파일을 놓을 경로 설정<br />
filename - 번들된 파일의 이름을 설정

#### 4) module - loaders
1. `Webpack` 에서는 `css`, 이미지 파일 등을 `Js` 모듈로 해석하는데, `Js` 모듈로 해석하는데 필요한 것들이 `loader` 이다.
2. `js` 파일에서 아래와 같이 `css` 파일 등을 불러올수 있는 재밌는 `import` 를 실행 할 수있다. 이외에도 `php`, `json`, `html` 등 
많은 파일을 `import` 및 `require` 할수 있다. (물론 `loader`로 해당 확장자 파일을 `Webpack`이 해석할 수있도록 세팅해야 한다.)
3. 앞에서 설명한 `babel` 을 주로 `Webpack`을 통해서 `loader` 설정을 통해 편리하게 사용할 수 있다.

```javascript
// app.js
require('../common.css');
import dataConfig from './data.json';
```
> `Webpack 2` 부터 `loaders` 옵션이 `rules` 나 `use`로 바뀌었고, 대신 `query` 옵션이 `options` 로 바뀌었다. `Webpack 2` 부터는 에러를 발생하니 참고바람.

#### 5) plugins
이름대로 `plugin`은 `Webpack` 에 여러가지 부가기능들을 제공해준다. 자주 사용하는 `plugin`은 위에 소스에 명시한 `html`, `css` 파일등을 압축하는
`plugin` 과 웹페이지를 새로고침없이 핫로딩 할수 있는 `HMR` 플러그인 등을 많이 사용하고 있다. 그외에 자신에게 필요한 기능을 찾아 입맛대로 골라 패키지를 설치하여 사용하면 된다.

```javascript
plugins: [
    new webpack.HotModuleReplacementPlugin(),
    new HtmlWebpackPlugin({
        template: './src/index.html'
    }),
    new MiniCssExtractPlugin({
        filename: "./css/common.css"
    })
]
```
#### 6) optimization
`Webpack 4` 에서 새로생긴 옵션이다. 파일 압축,난독,병합 등 압축관련 모듈들이 `optimization` 으로 병합되었다.
`minimize`가 `Webpack 2`의 `plugins` 에서 쓰던 `js`압축플러그인 `UglifyJsPlugin`을 포함하고 있고, `css` 압축플러그인 `OptimizeCSSAssetsPlugin`도 포함하고있다. 그 외에 사항은 [공식사이트](https://webpack.js.org/)에서 확인할 수 있다.

```javascript
optimization: { /* webpack 4에서 새로추가됨 */
    minimizer: [
        new UglifyJsPlugin({
            cache: true,
            parallel: true,
            sourceMap: true
        }),
        new OptimizeCSSAssetsPlugin({})
    ]
}
```

### 폴더 구조
```
| dist/
| src/
|   |- index.html
|   |- css/
|       |- common.scss
|   |-js/
|       |- index.js
|- package.json
|- webpack.config.js
```

### 설치
1. 터미널 사용을 위하여 전역으로 설치한다. (현재 4버전)<br />
`$ npm i -g webpack`

2. 로컬에서 개발모듈로 설치한다.<br />
`$ npm i -D webpack webpack-cli`

> `Webpack 4` 에서 기본적으로 `webpack-cli` 모듈을 설치하여야 한다.<br />
`Webpack 3` 까지는 `webpack`만 설치해도 되었는데 `Webpack 4` 부터는 `webpack-cli`를 같이 설치해야 `Terminal`에서 `webpack` 명령어를 사용할 수 있다.

3. 실행
`$ webpack --watch` (감시 모드)

### Webpack 에서 Babel 세팅하기

<img src="https://github.com//qnfzks55/webpack_lmj/blob/master/webpack_plus.jpg?raw=true" />

1. `babel` 설치를 해준다.<br />
`$ npm i -D babel-core babel-loader babel-preset-2015`
2. `loader`에 `babel-loader`를 추가하여 준다.

```javascript
{
    test: /\.js$/,
    exclude: /node_modules/,
    use: {
        loader: 'babel-loader',
        options: {
            babelrc: true,
            presets: ['es2015']
        }
    }
}
```
> 이외에도 [babel-polyfill](https://babeljs.io/docs/en/babel-polyfill/) 패키지를 추가적으로 설치하여 `ES6` 문법만 컴파일하여 사용하는게 아닌, `ES6` 의 새로운 객체들(`Promise`, `MAP` 등)을 컴파일하여 사용할 수 있다.

## Q&A

## 참고 링크
* [package.json 파일내의 dependencies와 devDependencies의 차이점](https://github.com/saeromCho/shumblr/wiki/package.json-%ED%8C%8C%EC%9D%BC-%EB%82%B4%EC%9D%98-dependencies%EC%99%80-devDependencies%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90%EA%B3%BC-%EC%B6%94%EA%B0%80%EC%A0%81%EC%9D%B8-%EA%B3%B5%EB%B6%80(About-Babel))
* [babel-preset](https://babeljs.io/docs/en/babel-preset-env/)
* [Ruby란](https://www.ruby-lang.org/ko/about/)
* [SCSS문법](https://soooprmx.com/archives/7948)
* [ZeroCho Blog](https://www.zerocho.com/)
* [웹팩 공식사이트](https://webpack.js.org/)
