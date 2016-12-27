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

> 참고

> 공식 사이트 : [http://jquery.com](http://jquery.com)

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

> 참고

> [안티패턴 - jQuery 같은 외부 소스는 다운로드해서 사용하라](https://github.com/nhnent/fe.javascript/wiki/%EC%95%88%ED%8B%B0-%ED%8C%A8%ED%84%B4#jquery-%EA%B0%99%EC%9D%80-%EC%99%B8%EB%B6%80-%EC%86%8C%EC%8A%A4%EB%8A%94-%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C%ED%95%B4%EC%84%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%9D%BC)

