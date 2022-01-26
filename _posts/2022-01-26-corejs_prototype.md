---
layout: post
title: "자바스크립트 코어 - 프로토타입"
description: "자바스크립트 코어의 프로토타입의 개념과 Constructor 프로퍼티의 개념"
date: 2022-01-26
tags: [study, js]
comments: true
share: true
---

## 자바스크립트 코어 - 프로토타입

## 목차

- [프로토타입의 개념](#프로토타입의-개념)
- [constructor 프로퍼티](#constructor-프로퍼티)
- [프로토타입 체인](#프로토타입-체인)
  - [메서드 오버라이드](#메서드-오버라이드)
  - [프로토타입 체인](#프로토타입-체인)
  - [객체 전용 메서드의 예외사항](#객체-전용-메서드의-예외사항)
  - [다중 프로토타입 체인](#다중-프로토타입-체인)
- [요약](#요약)

## 프로토타입의 개념
- 자바스크립트는 `prototype` 기반 언어임
- 클래스 기반 언어에서는 `상속`을 사용하지만 프로토타입 기반 언어에서는 `어떤 객체를 원형으로 삼고 이를 복제(참조)함` 으로써 상속과 비슷한 효과를 얻음

```js
var instance = new Constructor();
```
  - 어떤 생성자 함수(Constructor)를 new 연산자와 함께 호출
  - Constructor에서 정의된 내용을 바탕으로 새로운 인스턴스가 생성됨
  - 이때 인스턴스에는 `__proto__`라는 프로터티가 자동으로 부여
  - 이 프로퍼티는 Constructor의 프로토타입이라는 프로퍼티를 참조하게 됨
  - 프로토타입 객체 내부에는 인스턴스가 사용할 메서드가 저장되는데 그렇게 되면 인스턴스에서도 숨겨진 `__proto__`를 통해 메서드들에 접근할 수 있게 됨

```js
var Person = function(name) {
  this.name = name;
};
Person.prototype.getName = function() {
  return this.name;
};

var gildong = new Person('Gildong');
gildong.getName();  // Gildong
                    // __proto__ 는 생략이 가능함
gildong.__proto__.getName(); // undefined
                             // 함수를 메서드로서 호출했기 때문에 바로 앞의 객체가 this가 됨 
                             // __proto__ 객체에는 name 프로퍼티가 없기때문에 undefined 출력
Person.prototype === gildong.__proto__ // true
```

### 내장 생성자 함수 Array 예시
  ```js
  var arr = [1, 2];
  console.dir(arr);
  console.dir(Array);

  Array.isArray(arr);  // true
  arr.isArray();  // TypeError: arr.isArray is not a function
  ```
  - instance인 [1, 2]의 __proto__는 Array.prototype을 참조
  - isArray 정적 메서드는 프로퍼티 내부에 있지 않기 때문에 호출할 수 없음 (Array 생성자 함수에서 직접 접근해야 함)

## constructor 프로퍼티
- 생성자 함수의 프로퍼티인 Prototype 내부에는 `consturctor`라는 프로퍼티가 있음
- 인스턴스의 __proto__객체 내부에도 마찬가지. 이 프로퍼티는 단어 그대로 `자기자신을 참조`

```js
var arr = [1, 2];
Array.prototype.constructor === Array  // true
arr.__proto__constructor === Array  // true
arr.constructor === Array  // true

var arr2 = new arr.constructor(3, 4);
console.log(arr2)  // [3, 4]
```

- 예외적인 경우(기본형 리터널 변수가 부여된 경우)를 제외하고 constructor 값을 바꿀 수 있음
- 모든 데이터가 false를 반환하는데, constructor를 변경하더라도 참조하는 대상이 변경될 뿐 `이미 만들어진 인스턴스의
원형이나 데이터타입이 변하진 않음`
- 어떤 인스턴스의 생성자 정보를 알아내기 위해 constructor 프로퍼티에 의존하는 것이 항상 안전하지는 않다는 것을 알 수 있음

```js
var newConstructor = function () {
  console.log('this is new constructor!');
};

var dataTypes = [
  1,  // Number & false
  'test',  // String & false
  true,  // Boolean & false
  {},  // newConstructor & false
  new Number(),  // newConstructor & false
  new String(), // newConstructor & false
  new Boolean(), // newConstructor & false
  new Object(), // newConstructor & false
  new Array() // newConstructor & false
]; 

dataTypes.forEach(function (data) {
  data.constructor = newConstructor;
  console.log(data.constructor.name, '&', data instanceof newConstructor)
});
```

## 프로토타입 체인

### 메서드 오버라이드
- 인스턴스가 동일한 이름의 프로퍼티나 메소드를 가지게 되면 `메소드 오버라이드` 가 일어남
- 원본이 제거되는게 아니라 원본이 그대로 있는 상태에서 다른 대상을 그 위에 덮어씌움(오버라이드)

```js
var Person = function (name) {
  this.name = name;
}

Person.prototype.getName = function() {
  return this.name
};

var gildong = new Person('Gildong');

gildong.getName = function () {
  return '나는 ' + this.name;
};

console.log(gildong.getName());  // 나는 Gildong

/**
 * 자바스크립트 엔진이 getName 메서드를 찾을때 가장 가까운 대상인 자신의 프로퍼티를 검색하고 없으면 그 다음 대상인 __proto__를 찾음 그래서 undefined가 출력됨
*/

console.log(gildong.__proto__.getName());  // undefined

// call이나 apply 메서드를 이용하여 this 바인딩을 인스턴스를 바라보게 바꿔 줄 수 있음
console.log(gildong.__proto__.getName.call(gildong)); // Gildong
```

### 프로토타입 체인
- 배열 리터럴의 __proto__에 또다른 __proto__가 존재 함 (prototype의 객체가 말그대로 객체이기 때문)
- 모든 객체의 __proto__에는 Object.prototype이 연결됨 그러므로 Object.prototype이 언제나 프로토타입 체인 최상단에 존재함
- 배열 등은 객체의 내부 메서드를 `__proto__` 없이 실행할 수 있음

```js
var arr = [1, 2, 3];
arr.push(4);  // [1, 2, 3, 4]
arr.hasOwnProperty(1);  // true
```

> 프로토타입 체인 : 어떤 데이터의 `__proto__` 프로퍼티 내부에 다시 `__proto__` 프로퍼티가 연쇄적으로 이어진 것<br />
> 프로토타입 체이닝 : 프로토타입 체인을 따라가며 검색하는 것

### 객체 전용 메서드의 예외사항
- prototype은 객체이기 때문에 Object.prototype이 언제나 프로토타입 체인의 최상단에 존재함
- 그래서 객체에서만 사용할 메서드를 프로토타입 객체 안에 정의할 수 없음 (객체에서만 사용할 메서드를 Object.prototype 내부에 정의한다면 다른 데이터타입도 해당 메서드를 사용할 수 있게 되기 때문)
- 이러한 이유로 객체 전용 메서드는 Object.prototype이 아닌 Object에 `스태틱 메서드(static method)`로만 부여할 수 있음
- 반대로 같은 이유로, Object.prototype에는 어떤 데이터에서도 사용 가능한 범용적인 메서드들만 있음 (toString, valueOf 등은 변수가 마치 자신의 메서드인 것처럼 호출 가능)

> Static Method<br />
> - 클래스의 constructor(생성자)에 접근하지 않고 바로 static method를 실행하기 때문에 클래스를 생성하지 않고 클래스 내부에 바로 접근하여 실행이 가능<br />
> - constructor(생성자)에 선언된 변수, 객체 등 어떤 자료도 접근할 수 없다
> - 자세한 정보는 [여기 클릭](https://ko.javascript.info/static-properties-methods)

### 다중 프로토타입 체인
- 자바스크립트의 기본 내장 데이터 타입들의 프로토타입 체인은 사용자가 새롭게 정의한다면 무한대로 체인 관계를 이어나갈 수 있음
- __proto__가 가리키는 대상, 즉 생성자 함수의 prototype이 연결하고자 하는 상위 생성자 함수의 인스턴스를 바라보게끔 해주면 됨

```js
let Grade = function() {
  let args = Array.prototype.slice.call(arguments);
  for(let i = 0; i < args.length; i++) {
    this[i] = args[i];
  }
  this.length = args.length;
};
let g = new Grade(100, 80);
```
  - 변수 g는 Grade의 인스턴스를 바라봄 (Grade의 인스턴스는 배열의 메서드를 사용할 수 없는 유사배열객체임)
  - 이 인스턴스에서 배열 메소드를 직접 쓸 수 있게 하려면 g.`__proto__`, 즉 Grade.prototype이 배열의 인스턴스를 바라보게 하면 됨

  ```js
  Grade.prototype = [];

  let g = new Grade(100, 80);
  console.log(g);  // Grade(2) [100, 80]
  g.pop()
  console.log(g);  // Grade [100]
  g.push(90)
  console.log(g) // Grade(2) [100, 90]
  ```

## 요약
- 어떤 생성자 함수를 new 연산자와 함께 호출하면 Constructor에서 정의된 내용을 바탕으로 새로운 인스턴스가 생성되는데, 이 인스턴스에는 `__proto__` 라는, Constructor의 prototype 프로퍼티를 참조하는 프로퍼티가 자동으로 부여 됨
- __proto__는 생략 가능 속성이라 인스턴스는 Constructor의 메서드를 마치 자신의 메서드인 것처럼 호출할 수 있음
- Constructor.prototype에는 constructor라는 프로퍼티가 있는데 이는 생성자 함수 자기 자신을 가리킴 (이 프로퍼티는 인스턴스가 자신의 생성자 함수가 무엇인지 알고자 할 때 필요하지만 이미 만들어진 인스턴스의
원형이나 데이터타입이 변하지 않으므로 의존하면 안됨)
- __proto__방향을 계속 찾아가면 최종적으로 Object.prototype에 다다름
  - 이런 식으로 __proto__안에 다시 __proto__를 찾아가는 과정을 `프로토타입 체이닝`이라 함
  - 이런 특징을 통해 각 프로토타입 메서드를 `자신의 것`처럼 호출할 수 있음
- 프로토타입 체인은 반드시 1~2단계로만 이뤄지는 것이 아니라 무한대의 단계를 생성 가능
- Object.prototype에는 모든 데이터 타입에서 사용할 수 있는 범용적인 메서드만이 존재하며, 객체 전용 메서드는 여느 데이터타입과 달리 Object 생성자 함수에 static 하게 담겨있음