---
layout: post
title: "jQuery 가이드"
description: "jQuery 코딩 가이드 및 컨벤션 (펌)"
date: 2016-12-27
tags: [js, jQuery]
comments: true
share: true
---

## jQuery 가이드

***

jQuery는 파편화된 브라우저 환경에서 크로스브라우징 이슈를 쉽게 처리할 수 있도록 관련 API를 제공하는 자바스크립트 라이브러리로,
존 레식이 2006년에 공식적으로 소개하였으며, 오늘날 가장 인기있는 자바스크립트 라이브러리 중 하나이다.
DOM의 탐색과 조작이 주요한 기능이며 라이브러리에서 제공하지 않는 기능은 Plug-in을 통해 확장하여 구현할 수 있고,
자바스크립트 코드를 단순하게 유지하면서 크로스 브라우징 이슈를 보다 쉽게 처리할 수 있는 방법을 제공한다.

> 참고<br />
> 공식 사이트 : [http://jquery.com](http://jquery.com)<br />
> API Documentation : [http://api.jquery.com/](http://api.jquery.com/)

이 문서에서는 jQuery API에 대해 다루지 않는다.
대신 jQuery를 좀 더 효율적으로 사용할 수 있는 몇 가지 방법을 가이드 한다.

### 목차

* [설치하기](#%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0)
* [버전 선택하기](#%EB%B2%84%EC%A0%84-%EC%84%A0%ED%83%9D%ED%95%98%EA%B8%B0)
* [$ 식별자](#-%EC%8B%9D%EB%B3%84%EC%9E%90)
* [DOM 탐색](#dom-%ED%83%90%EC%83%89)
* [DOM 조작](#dom-%EC%A1%B0%EC%9E%91)
* [이벤트 처리](#%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EC%B2%98%EB%A6%AC)
* [메서드 체이닝](#%EB%A9%94%EC%84%9C%EB%93%9C-%EC%B2%B4%EC%9D%B4%EB%8B%9D)
* [Ajax](#ajax)

***

### 설치하기

jQuery는 하나의 js 파일로 구성되어 다운로드 및 사용이 쉽다.
필요한 버전의 jQuery를 [공식 사이트](http://jquery.com)에서 다운로드하여 사용하다.
jQuery에서 제공하는 외부 URL을 이용하는 방법도 있으나, 지양해야 한다.

> 참고<br />
[안티패턴 - jQuey 같은 외부 소스는 다운로드해서 사용하라](https://github.com/nhnent/fe.javascript/wiki/%EC%95%88%ED%8B%B0-%ED%8C%A8%ED%84%B4#jquery-%EA%B0%99%EC%9D%80-%EC%99%B8%EB%B6%80-%EC%86%8C%EC%8A%A4%EB%8A%94-%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C%ED%95%B4%EC%84%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%9D%BC)

### 버전 선택하기

크게 1.x 버전과 2.x 버전으로 나뉜다.<br>
두 버전 모두 파이어폭스, 구글 크롬, 사파리, 오페라 등의 다양한 브라우저를 지원하며<br>
각 브라우저의 최신 버전을 포함하여 이전 버전까지 안정적으로 지원한다.<br>

* 1.X 버전 : **IE6 및 그 이후 버전**을 지원
* 2.X 버전 : IE 6~8버전은 지원하지 않으며, **IE9 또는 그 이후 버전**을 지원

제공하는 서비스의 브라우저 지원 범위에 따라 jQuery 버전을 선택하여 사용해야 한다.

* **PC 서비스**의 경우 대부분 **1.X 버전(주로 1.8.3 버전)**을 사용 
* **모바일 서비스**의 경우 대부분 **2.X 버전**을 사용

1.7.0 이하 버전은 너무 오래된 버전이라 최신 플러그인 및 모던 브라우저와 충돌이 있으므로 사용하지 않도록 한다. 최신 버전은 이전 버전에 비해 성능이 향상되고 버그가 수정된 경우가 많기 때문에 가급적 최신 버전의 jQuery를 사용할 것을 권장한다.

### $ 식별자

jQuery는 한 개의 스크립트 파일로 이루어져 있음과 동시에 단 한 개의 함수로 구성되어 있다.
함수명은 jQuery이고, jQuery() 함수 한 개만 사용하면 jQuery의 모든 기능을 이용할 수 있다.
**$**라는 식별자를 사용하여 jQuery의 모든 명령어가 실행된다.
prototype과 같은 다른 자바스크립트 프레임워크를 이미 사용하고 있는 경우에는 $를 사용했을 때 오류가 발생할 수 있다.
이런 경우 $가 아닌 원래 함수인 jQuery를 사용하면 된다. <br>

### DOM 탐색

#### 가능하면 ID selector를 사용하라.

jQuery에서는 **document.getElementById()** 를 사용하기 때문에 ID selector가 빠르다. 하지만 가장 빠른 것은 native javascript 이다.

```javascript

// Fastest
document.getElementById("myId");

// Fast - still little slower than native
$("#myId");

// Slow
$('.myClass');

```