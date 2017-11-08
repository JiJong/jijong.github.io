---
layout: post
title: "Vue.js 시작하기"
description: "Vue.js Chapter.1"
date: 2017-11-08
tags: [study, js, vue.js, front-end]
comments: true
share: true
---

<img src="http://jijong.github.io/images/vuejs.png" width="250" height="250" style="margin: 0 auto" />

# Vue.js 시작하기

***

Vue.js는 최근 가장 빠르게 발전하고 확산되고 있는 프론트엔드 프레임워크중 신흥 강자로 떠오르 있는 대표적이 프레임워크이다.
아직은 `Angular.js` 나 `Reac.js` 보다 많이 알려지지 않았지만, 최근 급속도로 확산되고 있다.
[Github](https://risingstars2016.js.org/?ref=freecodecamp-loves-you#all)에서 star를 받은 수를 보면 vue.js의 인기를 실감할수 있다.
이번 블로그 포스트는 Vue.js가 무엇인가를 중점으로 포스트 하겠다. 기능들은 다음 학습 후에..
자, 그럼 Vue.js 가 무엇인지 알아보자.

### 목차

* [Vue.js 란?](#설치)
* [개발 환경 설정](#사용법)
* [Vue.js CLI](#webpackconfigjs-examples)
* [참고 링크](#참고-링크)

### Vue.js 란?

Vue.js는 Google Creative Lav에서 일하던 에반 유(Evan you)가 2013년 12월에 UI를 빠르게 개발하기 위해 만든 자바스크립트 프레임워크이다.
웹 화면 작성에 최적화된 `MVVM`패턴을 따르고 있다. Vue.js는 다른 프레임워크와 달리 굉장히 유연하고 가볍다. `Angular` 와 같이 전체 아키텍처를
새롭게 구성할 필요 없이 기존 웹 애플리케이션의 일부 UI화면만 적용하는 것이 가능하며, `SPA` 아키텍처 구성을 위 필수적으로 필요한 라우터 기능도
에코시스템을 통해 효과적으로 지원한다.

> MVVM 패턴은 Model - View - ViewModel 의 줄임말 이다.<br />
> MVVM 패턴은 애플리케이션 로직과 UI 로직의 분리를 위해 설계된 패턴이고, View는 HTML과 CSS로 작성하게 된다. ViewModel은 View의 실제 논리 데이터 흐름을 담당한다.

그리고, `jQuery` 처럼 `<script>` 태그를 이용하여 `CDN(Content Delivery Network)`상의 주소를 간단히 참조한 후 디렉티브만 익혀도 손쉽게 적용할 수 있다.
또한 `Vue-louter` 를 이용해 `SPA` 아키텍처 애플리케이션도 어렵지 않게 개발할 수 있고, `ES6` 와 `Webpack` 번들링을 통해 대규모 애플리케이션을 단일 파일 컴포넌트로 빌드할 수 있다.

### 개발 환경 설정

1. Node.js 설치
2. 크롬 엔진에서 제공하는 Vue.js devtools 설치

### Vue.js CLI

`Vue-CLI`는 에반 유가 공식적으로 관리하는 커맨드라인 인터페이스 기반의 스캐폴딩 도구 이다. 특히, Vue.js 앱을 개발할 때 프로젝트의 폴더 구조를
어떻게 잡을 것인지, 테스트, 빌드, 의존성 부분은 어떻게 설정할 것인지에 대한 고민을 하지 않도록 프로젝트의 기본 템플릿을 설정해주는 도구이다.

npm을 통해 `Vue-CLI`를 설치해 보자.

```javascript
$ npm install -g vue-cli
```

> Vue-CLI로 만들 수 있는 프로젝트 템플릿은 `vue list` 명령어를 실행하여 사용할 수 있는 프로젝트 템플릿을 확인해볼 수 있다.

#### Vue-CLI 템플릿 리스트

- simple : 가장 간단한 템플릿 유형으로 HTML 파일 하나만을 만들어 낸다. 내부에는 Vue.js를 CDN 방식으로 참조하고 있다.
- browserify : browserify + vueify 조합으로 hot-reload, linting, 단위 테스트를 지원하는 템플릿 유형이다.
- browserify-simple : 빠른 프로토타이핑을 위한 browserify_vueify가 설정된 간단한 템플릿 유형이다.
- webpack : webpack + vue-loader 조합의 기능에 hot-reload,lining, 단위 테스트를 지원하는 템플릿 유형이다.
- webpack-simple : 빠른 프로토타이핑을 위한 Webpack + vue-loader 가 설정된 간단한 템플릿 유형이다.
- pwa : PWA(Progressive Web App) 개발을 위한 템플릿 유형이다.

> browserify는 require()문 등으로 여러 개의 의존성 있는 자바스크립트 코드들을 참조하여 개발한 경우에 단일 자바스크립트 파일로 묶어주는 번들링 도구이다.

이 밖에도 다른 개발자들이 만든 템플릿을 내려받아 사용할 수도 있다.
Vue-CLI로 프로젝트 기본 틀을 만드는 방법은 다음과 같다.

```javascript
vue init [templet name][project name]
```

이 명령을 실행하면 project name으로 디렉터리가 생성 될것이다.
디렉터리 안에 생성된 파일을 열어서 개발을 시작하면 된다!

예제를 살펴보면,

#### 예제

```javascript
vue init simple hellovue
```

명령어를 실행 후 엔터키를 눌러 생성을 완료한다. 그리고 디렉토리 생성이 완료되었다면
명령창에서 hellovue 디렉토리로 들어가준다. `simple` 템플릿은 `index.html` 파일 하나만을 생성하기 때문에 테스트를 할때 사용하면 유용하다.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>02-01</title>
</head>
<body>
  <div id="app">
    <h2>{{message}}</h2>
  </div>
  <script src="https://unpkg.com/vue/dist/vue.min.js"></script>
  <script type="text/javascript">
    var model = {
      message : '안녕 Vue.js'
    };

    var app = new Vue({
      el : '#app',
      data : model
    })
  </script>
</body>
</html>
```

이상 Vue.js로 가장 간단한 애플리케이션을 만들어 보았다.
그럼 이제 소스에서 생소해 보이는 부분을 간략하게 살펴 보도록 하겠다.

```javascript
var model = {
  message : '안녕 Vue.js'
};
```

위 객체는 변수명 그대로 `Model` 객체이다. 데이터를 가지고 있다.

```javascript
var app = new Vue({
  el : '#app',
  data : model
})
```

`app` 객체는 `Vue` 객체이자 뷰모델 객체이다. `Vue` 객체의 `el` 속성은 HTML 요소를 나타낸다. 또한 `data` 속성은 모델 객체를 참조한다.
`Vue` 객체가 HTML요소와 데이터를 참조하고 있다. 이제 data(model)이 변경되면 뷰모델 객체는 즉시 HTML 요소(뷰)에 반영을 시키게 될것이다.

> HTML 요소에서는 `{{}}` 과 같은 콧수염을 닮은 모양의 템플릿 표현식을 사용한다. 이는 `jQuery` 템플릿과 같은 표현식이다. 이 표현식은 콧수염 모양을 닮았다고 해서 콧수염 표현식 또는
보간법이라고도 한다.

위 코드만으로 모든 작업은 반응형으로 이루어진다.<br />
지금까지 Vue.js가 무엇인지, 어떤 방식으로 작성되어지는지를 알아보았다. 나도 막 Vue.js 학습을 시작한 만큼
열심히 이해하고 학습해야 겠다..

### 참고 링크

- [Vue.js 공식 한국어 가이드](https://kr.vuejs.org/)
- [Vue.js 한국 사용자 모임](https://vuejs-kr.github.io/)
- [Vue.js 한국 페이스부 그룹](https://www.facebook.com/groups/1152461054807344/)
