---
layout: post
title: "자바스크립트 코어 - this"
description: "자바스크립트 코어의 this 바인딩과 명시적으로 this를 바인딩 하는 방법"
date: 2022-01-20
tags: [study, js]
comments: true
share: true
---

## 자바스크립트 코어 - this

## 목차

- [this란?](#this란?)
- [상황에 따라 달라지는 this](#상황에-따라-달라지는-this)
- [명시적으로 this를 바인딩하는 방법](#명시적으로-this를-바인딩하는-방법)
- [화살표 함수의 예외사항](#화살표-함수의-예외사항)
- [정리](#정리)

## this란?

- 대부분의 객체지향 언어에서는 this는 `클래스로 생성한 인스턴스 객체`를 의미함
- 자바스크립트에서의 this는 어디서든 사용 가능
- 함수와 객체(메서드)의 구분이 느슨한 자바스크립트에서 this는 이 둘을 구분하는 거의 유일한 기능

## 상황에 따라 달라지는 this

- 기본적으로 자바스크립트에서 this는 실행 컨텍스트가 생성될 때 함께 결정됨 (즉 this는 `함수를 호출할 때 결정`)
- 함수를 어떤 방식으로 호출하느냐에 따라 this가 바인딩하는 값이 달라짐

> 실행 컨텍스트 - 실행할 코드에 제공할 환경 정보들을 모아놓은 객체

### 1. 전역 공간에서의 this

- 전역 공간에서의 this는 `전역 객체`를 가리키고, 브라우저에서는 `window`를 Node.js에서는 `global` 객체를 가리킴
- 전역 공간에서 변수를 선언하면 전역객체인 (window, global)의 프로퍼티로 할당되고 자바스크립트의 모든 변수는 특정 객체의 프로퍼티로서 동작
- 전역 변수를 선언할때 처음부터 전역객체의 `프로퍼티로 할당`하면 삭제가 되지만, `전역 변수로 선언`하는 경우에는 delete 연산으로 삭제가 되지 않는다.

  ```js
  var a = 1; // 전역 변수 선언
  window.b = 1; // 전역객체의 프로퍼티로 할당

  delete a;
  delete window.b;

  console.log(a); // 1
  console.log(window.b); // undefined
  ```

### 2. 메서드로서 호출할 때 그 메서드 내부에서의 this

- 일단 함수와 메서드의 차이를 이해해야 함
  - 함수 : 독립적으로 수행할 수 있음
  - 메서드 : 자신을 호출한 대상 객체에 관한 동작을 수행함
- 함수를 객체의 프로퍼티로 할당한다고 무조건 메서드가 되는 것이 아니라 `객체의 메서드로서 호출`할 경우에만 메서드로 동작하고, 그렇지 않은 경우에는 `함수로 동작`
- 함수로서 호출과 메서드로서의 호출은 함수 앞에 `점(.)`이 있는지를 보거나 함수를 호출 할때 앞에 객체가 명시되어 있는지를 보면 쉽게 확인 가능

```js
var test = function () {
  console.log("CALL TEST()");
  console.log(this);
};

test(); // 함수로서 호출, this에 전역객체 호출

var object = {
  a: 1,
  test: test,
};

object.test(); // 메서드로서 호출, this에 object가 들어간다.
```

- 메서드 내부에서 호출 시 this에는 호출한 주체에 대한 정보가 담김
- 즉 함수 앞에 명시되어 있는 객체를 this가 가리키게 됨

### 3. 함수로서 호출할 때 그 함수 내부에서의 this

- 어떤 함수를 함수로서 호출할 경우에는 this가 지정되지 않음 (이때 this는 전역 객체를 바라보게 됨)
- 해당 함수를 호출하는 구문 앞에 점 또는 대괄호가 있다면 메서드 호출(this = 객체) 이고, 아니라면 함수(this = 전역객체)로 알면 됨
- this 바인딩에 관해서는 함수를 실행하는 주변환경(메서드 내부인지, 함수 내부인지)은 중요하지 않고, 오직 해당 함수를 호출하는 구문 앞에 `점 또는 대괄호 표기가 있는지 없는지`가 관건

#### 메서드의 내부 함수에서 this 우회하기

- 메서드 안에 함수에서 this가 전역객체를 바인딩 하지 않고 주변 환경의 this를 상속받아 사용하려면 `상위 스코프의 this`를 저장해서 내부함수에서 활용할 수 있음
- 이때 사람마다 _this, that, _ 등 제각각 다른 변수명을 쓰는데 self가 가장 많이 쓰이고 있음 (협업을 위해 가장 많이 쓰이는 단어를 활용)

```js
var test = {
  method_func: function () {
    console.log(this); // Method. Object를 바라본다.

    var func1 = function () {
      // 함수
      console.log(this); // 전역객체를 바라본다.
    };

    var self = this; // self에 this를 할당
    var func2 = function () {
      console.log(self); // 내부 함수 안에서 this를 사용할 수 있다.
    };
    func1();
    func2();
  },
  var1: 10,
  var2: 20,
};
test.method_func();
```

### 4. 콜백함수 호출 시 그 함수 내부에서의 this

- 먼저 콜백함수라 함은 함수 A의 제어권을 다른 함수(또는 메서드) B에게 넘겨주는 경우 함수 A를 말함
- 콜백함수도 함수이기 때문에 기본적으로 this가 전역객체를 참조
- 그러나 제어권을 받은 함수에서 콜백함수에 별도로 this가 될 대상을 지정한 경우에는 `그 대상을 참조`함 (ex. addEventListerner)

```js
setTimeout(function () {
  console.log(this);
}, 300); // 전역객체

[1, 2, 3, 4, 5].forEach(function (x) {
  console.log(this, x); // 전역객체와 배열요소가 5회출력
});

document.body.innerHTML += '<button id="a">클릭</button>';
document.body.querySelector("#a").addEventListener("click", function (e) {
  console.log(this, e); // 버튼 엘리먼트와 클릭 이벤트에 관한 객체가 출력
});
```

- `addEventListener` 메서드는 콜백함수를 호출할 때 자신의 this를 상속하도록 정의돼 있음 (즉 메서드명의 점(.) 앞부분이 곧 this가 됨)
- 콜백함수의 제어권을 특별히 정의하지 않은 경우에는 기본적으로 함수와 마찬가지로 `전역객체`를 바라보는것을 알 수 있음

## 명시적으로 this를 바인딩하는 방법

- 메서드, 함수 등의 상황별로의 this 바인딩 규칙을 깨고 this에 별도의 대상을 바인딩 하는 방법이라고 할 수 있음

### 1. call 메서드

```js
Function.prototype.call(thisArg[, arg1[, arg2[, ...]]])
```

- call 메서드의 첫 번째 인자를 this로 바인딩하고, 이후의 인자들은 호출할 함수의 매개변수로 사용함
- 즉, 함수를 그냥 실행하면 this에는 전역객체가 할당되지만 call 메서드를 이용하면 임의로 this를 할당 할 수 있음

```js
var func = function () {
  console.log(this);
};

func(); // 전역객체가 찍힌다.
func.call({ a: 10, b: 20 }); // { a: 10, b: 20 }
```

### 2. apply 메서드

```js
Function.prototype.apply(thisArg[, argsArray])
```

- call 메서드와 동일함 하지만 apply 메서드는 두번째 인자로 배열을 받는데, 해당 `배열 요소`를 함수의 매개변수로 사용하는 차이점이 있음
- apply 메서드의 첫번째 인자를 this로 바인딩하고, 이후 배열에 있는 요소를 함수의 매개변수로 사용

```js
var func = function(a, b, c) {
  console.log(this, a, b, c);
};
func.apply({ x: 1 }, [4, 5, 6]); // { x: 1 } 4 5 6

var obj = {
  a: 1,
  method: function(x, y) {
    console.log(this.a, x, y);
  },
};
obj.method.apply({ a: 4 }, [5, 6]); // 4 5 6
```

### 3. bind 메서드

```js
Function.prototype.bind(thisArg[, arg1[, arg2[, ...]]])
```

- ES5에서 추가된 기능으로, call과 비슷하지만 즉시 호출하지 않고 넘겨 받은 this 및 인수들을 바탕으로 `새로운 함수를 반환`
- bind 메서드는 함수에 this를 미리 적용하는 것과 부분 적용 함수를 구현하는 두 가지 목적으로 사용됨
- bind 메서드를 사용하여 만들어진 함수의 경우 name 프로퍼티에 `bound`라는 접두어가 붙은 bind 메서드를 적용한 새로운 함수라는 의미로 기존의 call 이나 apply 보다 코드 추적이 용이함

```js
var func = function(a, b, c, d) {
  console.log(this, a, b, c, d);
};
func(1, 2, 3, 4); // Window{ ... } 1 2 3 4

var bindFunc1 = func.bind({ x: 1 }); // bind는 this만을 지정
bindFunc1(5, 6, 7, 8); // { x: 1 } 5 6 7 8

var bindFunc2 = func.bind({ x: 1 }, 4, 5); // this 지정과 함께 부분 적용 함수
bindFunc2(6, 7); // { x: 1 } 4 5 6 7
bindFunc2(8, 9); // { x: 1 } 4 5 8 9

console.log(bindFunc2.name); // bound func
```

## 화살표 함수의 예외사항
- `ES6`에 새로 도입된 화살표 함수(Arrow Function)는 실행 컨텍스트 생성 시 this 바인딩하는 과정이 제외됨
- 즉 이 함수 내부에는 this가 없고, 접근하고자 하면 스코프체인상 가장 가까운 this에 접근하게 됨
- 화살표 함수를 쓰면 변수로 this를 우회하거나 call/apply/bind 메서드를 적용할 필요가 없어 더욱 간결하고 편리함

## 정리
- 상황별 this 바인딩
  - 전역공간에서의 this는 전역객체(브라우저에서는 `window`, Node.js에서는 `global`)을 참조
  - 함수를 메서드로서 호출한 경우 this는 `메서드 앞의 객체`를 참조
  - 함수를 함수로서 호출한 경우 this는 `전역객체`를 참조 (메서드 내부함수에서도 같음)
  - 콜백함수 내부에서의 this는 해당함수의 제어권을 넘겨받은 함수가 정의한 바를 따르고, 그렇지 않으면 `전역객체`를 참조

- 명시적 this 바인딩
  - call, apply 메서드는 this를 명시적으로 지정하면서 함수 또는 메서드 호출
  - bind 메서드는 this 및 함수에 넘길 인수를 일부 지정해서 새로운 함수를 만듦
