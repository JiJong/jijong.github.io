---
layout: post
title: "Postman에서 POST http 메소드 날려 데이타 확인하기"
description: "Webpack으로 자동화 프론트엔드 개발환경 구축하기"
date: 2021-12-18
tags: [front-end]
comments: true
share: true
---

# Postman에서 POST http 메소드 날려 데이타 확인하기

***

오랜만에 포스팅 한다. 기초적인 부분이지만 Postman 사용 시 참고 차 포스팅 하였다.

* http 메소드를 POST 로 설정 후 send 를 누르면 아래 사진과 같이 `400 Bad Request` 상태코드를 확인할 수 있음
  * Request Body 에서 요청한 데이타와 일치하도록 서버가 예상하는 형식으로 전송해줘야 함

<img src="http://jijong.github.io/images/postman_1.png" />

> 400 Bad Request : 요청한 데이타가 서버 측 데이타와 그 형식이 일치 하지 않을 때를 의미

* Headers 에서 key/value 값 세팅
  * key : `Content-Type`
  * value : `application/json`

<img src="http://jijong.github.io/images/postman_2.png" />

* Body 에서 raw를 선택하고 형식이 JSON 으로 선택되어 있는지 확인 후 파라미터값 입력

<img src="http://jijong.github.io/images/postman_3.png" />