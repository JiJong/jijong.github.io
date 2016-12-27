---
layout: post
title: "jQuery 가이드"
description: "jQuery 코딩 가이드 및 컨벤션 (펌)"
date: 2016-12-27
tags: [js, jQuery]
comments: true
share: true
---

## jQuery 코딩 컨벤션 가이드

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

* [설치하기](#section-1)
* [버전 선택하기](#section-2)
* [$ 식별자](#section-3)
* [DOM 탐색](#dom-)
* [DOM 조작](#dom--1)
* [이벤트 처리](#section-4)
* [메서드 체이닝](#section-6)
* [Ajax](#ajax)

***

### 설치하기


jQuery는 하나의 js 파일로 구성되어 다운로드 및 사용이 쉽다.
필요한 버전의 jQuery를 [공식 사이트](http://jquery.com)에서 다운로드하여 사용하다.
jQuery에서 제공하는 외부 URL을 이용하는 방법도 있으나, 지양해야 한다.

> 참고<br />
[안티패턴 - jQuey 같은 외부 소스는 다운로드해서 사용하라](https://github.com/nhnent/fe.javascript/wiki/%EC%95%88%ED%8B%B0-%ED%8C%A8%ED%84%B4#jquery-%EA%B0%99%EC%9D%80-%EC%99%B8%EB%B6%80-%EC%86%8C%EC%8A%A4%EB%8A%94-%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C%ED%95%B4%EC%84%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%9D%BC)

### 버전 

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

jQuery에서는 `document.getElementById()` 를 사용하기 때문에 ID selector가 빠르다. 하지만 가장 빠른 것은 native javascript 이다.

```javascript
// Fastest
document.getElementById("myId");

// Fast - still little slower than native
$("#myId");

// Slow
$('.myClass');
```

#### class selector를 사용할 때에는 element type을 selector 앞에 사용하지 마라.

```javascript
// Fast
var $products = $('.products');

// Slow
var $products = $('div.products');
```

#### 특정 id를 기준으로 자식 element 목록을 탐색할 때는 .find()를 사용하라. Sizzle selector engine를 거치지 않기 때문에 빠르다.

```javascript
// Good - #products is already selected by document.getElementById() so only div.id needs to go through Sizzle selector engine
var $productIds = $('#products').find('div.id');

// Bad - a nested query for Sizzle selector engine
var $productIds = $('#products div.id');
```

#### selector를 최적화하라.

가능하다면 selector의 최우측은 "tag.class"를, 좌측엔 "tag" 또는 ".class"로 조합하면 빠르다.

```javascript
// Optimized
$('.data td.gonzalez');

// Unoptimized
$('div.data .gonzalez');
```

#### 복잡한 selector는 피하라.

```javascript
// Better
$('.data td.gonzalez');

// Normal
$('.data table.attendees td.gonzalez');
```

#### 탐색 범위를 좁힐 수 있도록 selector에 context 정보를 제공하라.

```javascript
// Faster - because now it only looks under class-container
$('.class','#class-container'); 

// Slower - because it has to traverse the whole DOM for .class
$('.class'); 
```

#### 전역 selector는 피하라.

```javascript
// Much better
$('.buttons').children();
// Extremely expensive
$('.buttons > *');

// Much better
$('.category input:radio'); 
// Implied universal selection
$('.category :radio');
// Same thing - explicit now
$('.category *:radio'); 
```

#### selector를 명확하게 사용하라.

selector를 생략하는 경우 이는 전역 selector를 사용하는 것과 다를바 없다.

```javascript
// Good
$('div.someclass input:radio');

// Bad
$('div.someclass :radio');
```
 
#### ID selector를 사용할때는 다른 것과 같이 사용하지 마라.

document.getElementById()를 사용하기 때문에 혼합해서 사용하면 빠르지 않다.

```javascript
// Good - only calls document.getElementId();
$('#inner');

// Bad
$('#outer #inner');
// Bad
$('idv#inner'); 
// Bad
$('.outer-container $inner');
```

### DOM 조작

#### 이미 존재하는 element를 조작하기 전에는 항상 detach하라.

```javascript
var $myList = $('#list-container > ul').detach();
//...a lot of complicated things on $myList
$myList.appendTo('#list-container');
```

#### append()를 보다 string concatenation 또는 array.join()을 사용하라.

```javascript
// Even faster
var i = 0,
    array = [];
for(; i < 10000; i++){
    array[i] = '<li>' + i + '</li>';
}
$myList.html(array.join(''));

// Good
var $myList = $('#list'),
    list = '',
    i = 0;
for(; i < 10000; i++){
    list += '<li>' + i + '</li>';
}
$myList.html(list);

// Bad
var $myList = $('#list');
for(var i = 0; i < 10000; i++){
    $myList.append('<li>' + i + '</li>';);
}
```

#### element의 유무를 확인하고 실행하라.

```javascript
// Good
var $mySelection = $('#nosuchthing');
if ($mySelection.length) {
    $mySelection.slideUp();
    ...
}

// Bad - This runs three functions before it realizes there's nothing in the selection
$('#nosuchthing').slideUp();
```

#### jQuery에 css 스타일을 섞어서 직접 사용하지 마라.

css에서 class를 정의하고, 자바스크립트에서 class를 추가, 삭제, 수정하여 스타일을 조작한다.

```css
/* Good */
.error { color: red; font-weight: bold; }
```

```javascript
// Good
$("#mydiv").addClass("error");

// Bad
$("#mydiv").css({'color':red, 'font-weight':'bold'});
```

### 이벤트 처리

#### HTML 마크업에 직접 이벤트를 걸지 마라.

디버깅이 어렵고, 동적으로 쉽게 이벤트를 생성하고 삭제하는 것이 어렵다.

```javascript
// Good
$('#myLink"').on('click', myEventHandler); 
```
```html
<!-- Bad -->
<a id="myLink" href="#" onclick="myEventHandler();">my link</a>
```

#### 이벤트 위임을 사용하라.

이벤트 위임(Event delegate)을 사용하면 동적으로 추가 또는 수정되는 자식 엘리먼트들의 이벤트도 함께 처리할 수 있는 이점이 있다.<br>

```javascript
$("#parent-container").on("click", "a", delegatedClickHandler);
```

#### event handler에 익명 함수를 사용하지 마라.

익명 함수를 사용하면 디버깅과 관리 그리고 테스트가 어렵다.

```javascript
// Good
function myLinkClickHandler(){...}
$('#myLink').on('click', myLinkClickHandler);

// Bad
$('#myLink').on('click', function(){...}); 
```

#### 한 페이지에 하나의 ready event handler만 사용하라.

디버깅이 용이하며 동작의 흐름도 추적할 수 있다.

#### ready event handler에 익명 함수를 사용하지 마라.
익명 함수를 사용하면 디버깅과 관리 그리고 테스트가 어렵다.

```javascript
// Good
$(document).ready(initPage);
function initPage(){
    // Page load event where you can initialize values and call other initializers.
}

// Bad - You can never reuse or write a test for this function
$(function(){ ... });
```

#### ready event handler는 자바스크립트 파일을 모두 로드한 후 외부 파일 인라인에서 포함되어 실행되어야 한다.

```html
<script src='my-document-ready.js'></script>
<script>
    // Any global variable set-up that might be needed.
    $(document).ready(initPage);
</script>
```

#### 사용자 정의 이벤트는 unbind가 용이하도록 namespace를 사용하라.

```javascript
// Good
$('#myLink').on('click.mySpecialClick', myEventHandler); 

// Later on - it's easier to unbind just your click event
$('#myLink').unbind('click.mySpecialClick');
```

### 메서드 체이닝

#### 메서드 체이닝을 사용하라.

메서드 체이닝은 변수 캐싱 및 selector를 여러번 호출하지 않아도 되는 이점이 있다.

```javascript
$('#myDiv').addClass('error').show();
```

#### 메서드 체이닝을 3번 이상하면 가독성에 문제가 있으니 줄바꿈을 사용하라.

```javascript
$('#myLink')
    .addClass('bold')
    .on('click', myClickHandler)
    .on('mouseover', myMouseOverHandler)
    .show();
```

#### 같은 메서드를 2번 이상 사용할 경우에는 메서드 체이닝보다는 객체 리터럴을 사용하라.

```javascript
// Good
$myLink.attr({
    href: '#',
    title: 'my link',
    rel: 'external'
});

// Bad
$myLink.attr('href', '#').attr('title', 'my link').attr('rel', 'external');
```

### Ajax

#### getJson() 또는 get()의 사용을 피하라.

내부적으로 무엇이 호출되는지와 상관없이 간단하게 $.ajax()를 사용한다.

#### request url에는 프로토콜을 명시하지 마라.

schemaless URL을 사용하여 브라우저 자동으로 판단하도록 맡긴다.

#### request시 파라메터는 url에 붙여서 사용하지 말고, data 객체를 사용하라.

가독성이 좋아지고 디버깅이 쉬워진다.

```javascript
// Good
$.ajax({
    url: 'something.php',
    data: { 
        param1: test1, 
        param2: test2 
    }
});

// Bad
$.ajax({
    url: 'something.php?param1=test1&param2=test2',
    ....
});
```

#### 필요한 데이터 타입을 명확히 알 수 있도록 dataType을 명시하라.

```javascript
var jqxhr = $.ajax({
    url: url,
    ...
    dataType: 'json',           // specify the dataType for future reference
    ...
});
```

#### Promise 인터페이스를 사용하면 가독성 및 동작의 흐름을 이해하는데 도움이 된다.

```javascript
$.ajax({ ... }).then(successHandler, failureHandler);
```
또는

```javascript
var jqxhr = $.ajax({ ... });
jqxhr.done(successHandler);
jqxhr.fail(failureHandler);
```

#### Ajax 템플릿 예제

```javascript
var jqxhr = $.ajax({
    url: url,
    type: 'GET',             // default is GET but you can use other verbs based on your needs
    cache: true,             // default is true, but false for dataType 'script' and 'jsonp', so set it on need basis 
    data: {},                // add your request parameters in the data object
    dataType: 'json',        // specify the dataType for future reference
    jsonp: 'callback',       // only specify this to match the name of callback parameter your API is expecting for JSONP requests
    statusCode: {            // if you want to handle specific error codes, use the status code mapping settings
        404: handler404,
        500: handler500
    }
});
jqxhr.done(successHandler);
jqxhr.fail(failureHandler);
```