---
layout: post
title: "ECMAScript 정리"
description: "ECMAScript의 탄생과 버전벌 특징들을 정리함"
date: 2022-01-13
tags: [study, js]
comments: true
share: true
---

## ECMAScript 정리

자바스크립트의 탄생과 역사, ECMAScript 이하 ES가 무엇인지 정의와 각 버전별 특징&차이점을 간략하게 정리하였다.
최신 스펙의 기능 등 세세한 부분은 참조한 링크에 잘 정리가 되어있어 해당 글에는 따로 정리는 하지 않았다.

### 목차

- [JavaScript의 탄생](#JavaScript의-탄생)
- [ECMAScript 설명](#ECMAScript-설명)
- [ECMAScript 버전별 특징](#ECMAScript-버전별-특징)
- [참고 자료](#참고-자료)

### JavaScript의 탄생

---

- 자바스크립트는 1995년 넷스케이프에서 일하고 있던 브랜든 아이크에 의해 만들어졌음
- 최초의 자바스크립트는 `Mocha`라는 이름으로 발표가 되었다가 이 후 `LiveScript`라는 이름을 거쳐 최종적으로 `Javascript`라는 이름을 갖게 되었음
- Java와는 아무 연관이 없지만, 당시 Java의 유명세에 묻어가려는 마케팅적 이유로 이름이 붙여짐

### ECMAScript 설명

---

- ECMAScript는 [ECMA 인터내셔널](https://www.ecma-international.org/)에 의해 제정되어 [ECMA-262](https://www.ecma-international.org/publications-and-standards/standards/ecma-262/) 기술 규격에 정의된 JavaScript와 같은 `인터프리터`, `스크립트 언어`의 표준을 말함
- 표준을 위해 자바스크립트를 ECMA 인터내셔널에 제출하였고 표준에 대한 작업을 **ECMA-262**란 이름으로 1996년 11월에 시작해서 1997년 6월에 채택 됨
- ES뒤에 년도가 아닌 숫자가 붙는 것은 버전 단위로 붙은 버전형 명칭 (매년 기능의 확장과 버전업으로 현재는 ES2020과 같이 뒤에 년도를 붙이는 것을 기본 버전명으로 사용)
- 매년 6월에 새 규격이 나오고 있기 때문에 2020년 6월에 나온 버전은 `11`버전이 되고, `ES2020`이 됨

### ECMAScript 버전별 특징

---

##### 스크립트 언어의 표준화 제정 필요

- **브라우저마다 스크립트 언어가 다르기 때문에 서로 호환이 되지 않고 파편화가 되기 시작함**
- 자바스크립트를 개발한 넷스케이프에서는 96년 11월 브라우저에서 돌아가는 스크립트 언어를 표준화하기 위해 ECMA 인터내셔널(국제표준화기구)에 자바스크립트 기술 규격 제정을 요청함
- ECMA 인터내셔널에서는 넷스케이프가 제안한 자바스크립트 기술규격을 `ECMA-262` 라는 이름으로 표준화 작업 시작

---

<aside>
📌 **ECMA 인터내셔널**                                                                                                                             - C++, C#, CLI, 파일구조, JSON 등 다양한 표준을 제정하는 기구                                                                                                                  - 과거에는 유럽 컴퓨터 제조 협회였으나, 지금은 유럽 뿐 만 아니라 전 세계적인 표준화 작업을 하는 국제 표준화 기구

</aside>

---

##### ES1 ~ ES3 (1997 ~ 1999)

- 97년 `ES1`을 시작으로 98년 `ES2`, 99년 `ES3`가 발표됨
- ES3에서는 `try/catch` 문법이 들어감
- 자바스크립트 기본적인 특징
  - 호이스팅 - 자바 스크립트 Parser가 함수 내에서 아래쪽에 존재하는 내용 중 필요한 값들을 끌어올리는 것
  - 프로토타입
  - 함수 단위의 스코프
  - 모듈화 미지원
  - 클로져 - 내부함수가 외부함수의 맥락(context)에 접근할 수 있어, private하게 사용 가능, 모듈화 시키기 위함도 있음.
  - Try / Catch - 예외처리
  - 정규식 - 문자열을 검색하고 대체하는 데 사용 가능한 일종의 형식 언어

##### ~~ES4 (폐기)~~

- ~~이 후 ES4 표준 작업이 진행되었지만 언어에 얽힌 정치적인 견해 차이로 ES4 명세는 폐기됨~~

##### ES5 (2009)

##### [목록]

- 배열에 `forEach`, `map`, `filter`, `reduce`, `some`, `every` 와 같은 메서드 지원
- `Object`에 대한 `getter` / `setter` 지원
  - **get** : 프로퍼티를 읽으려고 할 때 실행 , **set** : 프로퍼티에 값을 할당하려 할 때 실행
- 자바스크립트 `strict` 모드 지원
- `JSON` 지원 (과거에는 XML을 사용하다가, json을 많이 사용하면서 지원하게 됨)
- this를 강제로 bind 시켜주는 `bind()` 메서드 지원
- IE의 J스크립트는 아직도 `addEventListner`와 `attachEvent` 같은 J스크립트만의 문법을 사용하는 등 여전히 `Cross-browsing` 문제가 발생하고 있었음
  ##### 1) Strict 모드 지원
  - ’**strict mode**‘에서 javascript code를 실행한다.
  - script나 function 시작 부분에 **“use strict;”** 을 선언함으로써 사용
  - 선언하지 않은 변수, 객체의 사용/수정/삭제를 할 수 없다.
  - **IE9에서는 지원하지 않음.**
  [[주요 배열 메서드 (Array)]](https://www.notion.so/680e3a3ae24e4719a7ecdbad20cf4498)
  [[주요 객체 메서드 (Object)]](https://www.notion.so/11b24b2c15894c5988b9d097f67de7cd)

##### ES6 (2015)

##### [목록]

- `ECMAScript2015` 라고도 하며 MS에서는 ECMAScript를 표준을 최대한 따르는 `IE Edge`를 발표함
- 템플릿 리터럴 (Template literals)
- 화살표 함수 (Arrow Function)
- This
- 변수 선언 (Variable) - Let, const
- 모듈 (Module) - Import, Export
- 클래스 (Class)
- 가변 파라미터
  ##### 1) 템플릿 리터럴 (Template literals)
  - ES6부터 새롭게 등장한 템플릿 리터럴로 문자열 표현이 훨씬 간단해짐
  - 여러 줄로 이뤄진 문자열과 문자 보간기능을 사용할 수 있음
  - 이중 따옴표나 작은 따옴표 대신 `백틱`을 사용함
  - 플레이스 홀더를 이용하여 표현식을 넣을 수 있는데 플레이스 홀더는 `${expression}`으로 표기할 수 있음
    ##### ES5
    ```jsx
    var name = "john";
    var age = 60;
    console.log("저의 이름은 " + name + "이고, 나이는 " + age + "살 입니다.");
    ```
    ##### ES6
    ```jsx
    var name = "john";
    var age = 60;
    console.log(`저의 이름은 ${name}이고, 나이는 ${age}살 입니다.`);
    ```
  ##### 2) 화살표 함수 (Arrow Function)
  - function 키워드 대신 화살표(=>)를 사용하여 간략하게 사용할 수 있음
  - this를 바인딩 하지 않고 **선언된 함수 내부의 scope의 this를 가리킴**
  - **익명 함수**로만 사용할 수 있음
    → 따라서 화살표 함수를 호출하기 위해서는 함수 표현식을 사용 (콜백함수로도 사용할 수 있음)
    ##### ES5
    ```jsx
    // 익명함수
    var pow = function (x) {  return x * x;};
    console.log(pow(10)); // 100

    // 콜백함수 (함수표현식 보다 표현이 간결)
    var arr = [1, 2, 3];
    var pow = arr.map(function (x) {
    	// x는 요소값  return x * x;}
    );
    console.log(pow); // [ 1, 4, 9 ]
    ```
    ##### ES6
    ```jsx
    // 익명함수
    const pow = (x) => x * x;
    console.log(pow(10)); // 100

    // 콜백함수 (함수표현식 보다 표현이 간결)
    const arr = [1, 2, 3];
    const pow = arr.map((x) => x * x);
    console.log(pow); // [ 1, 4, 9 ]
    ```
  ##### 3) This
  - function 키워드로 생성한 일반 함수와 화살표 함수의 가장 큰 차이점
  - ES5같은 경우 객체 내에 있는 메서드를 실행 시 this는 메서드가 선언된 해당 객체를 가리킴
  - ES6에서의 this 는 자신을 둘러싸고 있는 this를 바라보기 때문에 따로 바인딩이나 변수에 담을 필요 없음
  - 화살표 함수의 this는 언제나 상위 스코프의 this를 가리킴
  - 화살표 함수는 call, apply, bind 메서드를 사용하여 this를 변경할 수 없음
    ```jsx
    var obj = {
    	value: 10,

      // 메소드 호출
      show: function () {
        console.log(this.value); // 10

        // 함수 호출
        function show_01 () {
          console.log(this.value); // undefined
        }
        show_01();

        // 화살표 함수
        function show_02 = () => {
          console.log(this.value); // 10
        }
        show_02();
      }
    }
    ```
  ##### 4) 변수 선언 (Variable)
  - ES5에선 `var` 밖에 존재하지 않았으며 var 는 변수를 선언할 때 사용되는 키워드임
  - **재할당과 재선언에 자유로움**
  - ES6부터 `let`, `const` 키워드가 추가됨
    ##### ES5
    ```jsx
    x = 15;
    console.log(x); //15
    var x = 12;
    console.log(x); //12

    // var는 Function 스코프는 내부에 선언된 var를 외부에서 참조할 수 없지만 블록 스코프에선 내부에 선언되어 있어도 외부에서 참조 가능
    function f() {
      var v = 5;

      console.log(v); // 5
    }

    console.log(v); // ReferenceError: v is not defined

    if (true) {
      var i = 0;
    }

    console.log(i); // 0
    ```
    ##### ES6
    ```jsx
    // let은 한번 선언된 변수에 동일한 이름으로 선언할 수 없음 하지만 값은 재할당 할 수 있음
    let x = 10;
    x = 15;
    console.log(x); //15
    let x = 12; // Identifier 'x' has already been declared

    // const는 한번 초기화된 변수에 재할당/재선언할 수 없음
    const x = 10;
    console.log(x); // 10;
    x = 15; // TypeError: Assignment to constant variable.

    // let, const는 블록 스코프 또는 Function 스코프 내부에 선언되면 해당 스코프 밖에서 안에 있는 변수를 참조할 수 없음
    if (true) {
      var i = 0;
    }
    console.log(i); // 0

    if (true) {
      let j = 10;
    }
    console.log(j); // ReferenceError

    if (true) {
      const k = 100;
    }
    console.log(k); // ReferenceError
    ```
  - 위 내용을 정리하면 다음과 같음
    [변수별 특징](https://www.notion.so/077f0921520845a8ba87a4914f215111)
  ##### 5) 모듈 (Module)
  - ES5 에선 `require` 를 통해 모듈화 했음
    ```jsx
    // 파일 자체를 사용할 수 있음
    var slider = require(./slider.js)
    // 혹은 require(./slider)
    ```
  - ES6 부터는 `import/export`로 모듈을 관리 가능
  - 클래스와 같은 모듈이 로딩될때, import와 export를 이용해 사용함
  - `**export` 키워드로 변수, 함수, 클래스를 외부의 스크립트로 모듈화 시킬 수 있음\*\*
  - 비동기 방식으로 작동하고 **모듈에서 실제로 쓰이는 부분만 불러오기 때문에 성능과 메모리 부분에서 유리함**
  - 외부로 보내고 싶은 것들에 일일이 키워드를 붙여도 되고 아래처럼 한번에 export 해도됨
    ```jsx
    const pi = Math.PI;

    function square(x) {
      return x * x;
    }
    class Person {
      constructor(name) {
        this.name = name;
      }
    }
    export { pi, square, Person };
    ```
  - 내보내기
    ```jsx
    const exchangeRate = 0.91;

    // 안 내보냄
    function roundTwoDecimals(amount) {
      return Math.round(amount * 100) / 100;
    }

    // 내보내기 1
    export function canadianToUs(canadian) {
      return roundTwoDecimals(canadian * exchangeRate);
    }

    // 내보내기 2
    const usToCanadian = function (us) {
      return roundTwoDecimals(us / exchangeRate);
    };
    export { usToCanadian };
    ```
  - 불러오기
    ```jsx
    // Destructuring
    import { canadianToUs } from "./currency-functions";

    console.log("50 Canadian dollars equals this amount of US dollars:");
    console.log(canadianToUs(50));

    // Alias
    import * as currency from "./currency-functions";

    console.log("30 US dollars equals this amount of Canadian dollars:");
    console.log(currency.usToCanadian(30));
    ```

##### 6) 클래스 (Class)

- ES5에선 `class`라는 키워드는 없었지만 생성자 함수와 프로토타입, 클로저를 사용하여 객체 지향 프로그래밍을 구현함
  ```jsx
  var Add = function (arg1, arg2) {
    this.arg1 = arg1;
    this.arg2 = arg2;
  };

  Add.prototype.calc = function () {
    return this.arg1 + "+" + this.arg2 + "=" + (this.arg1 + this.arg2);
  };

  var num = new Add(5, 8);
  console.log(num.calc()); // 5 + 8 = 13
  ```
- ES6에서는 `class` 키워드를 사용해서 선언 가능
- class는 class 선언문 이전에 참조할 수 없음
  ```jsx
  class Add {
    constructor(arg1, arg2) {
      this.arg1 = arg1;
      this.arg2 = arg2;
    }
    calc() {
      return this.arg1 + "+" + this.arg2 + "=" + (this.arg1 + this.arg2);
    }
  }

  var num = new Add(5, 8);
  console.log(num.calc()); // 5 + 8 = 13
  ```
- 마치 생성자 함수와 같이 **new 연산자와 함께 클래스 이름을 호출하면 클래스의 인스턴스가 생성**됨
  ```jsx
  class Foo {}
  const foo = new Foo();
  ```
- 위 코드에서 new 연산자와 함께 호출한 Foo는 클래스의 이름이 아니라 `constructor(생성자)`이다.
  표현식이 아닌 선언식으로 정의한 클래스의 이름은 `constructor`와 동일함
  ```jsx
  class Foo {}
  const foo = new Foo();
  ```
  ##### [getter]
  - `getter`는 클래스 필드에 접근할 때마다 **클래스 필드의 값을 조작하는 행위가 필요할 때 사용**
  - `getter`는 메소드 이름 앞에 `**get` 키워드\*\*를 사용해 정의함
  - 이때 메소드 이름은 클래스 필드 이름처럼 사용됨
    → 다시 말해 `getter`는 호출하는 것이 아니라 **프로퍼티처럼 `참조`하는 형식으로 사용**하며 참조 시에 메소드가 호출됨
  - `getter`는 이름 그대로 무언가를 취득할 때 사용하므로 **반드시 무언가를 반환**해야 함
    ```jsx
    class Foo {
      constructor(arr = []) {
        this._arr = arr;
      }

      // getter: get 키워드 뒤에 오는 메소드 이름 firstElem은 클래스 필드 이름처럼 사용된다.
      get firstElem() {
        // getter는 반드시 무언가를 반환해야 한다.
        return this._arr.length ? this._arr[0] : null;
      }
    }

    const foo = new Foo([1, 2]);
    // 필드 firstElem에 접근하면 getter가 호출된다.
    console.log(foo.firstElem); // 1
    ```
  ##### [setter]
  - `setter`는 클래스 필드에 **값을 할당할 때마다 클래스 필드의 값을 조작하는 행위가 필요할 때 사용**
  - `setter`는 메소드 이름 앞에 `**set` 키워드\*\*를 사용해 정의함
  - 이때 메소드 이름은 클래스 필드 이름처럼 사용됨
    → 다시 말해 setter는 호출하는 것이 아니라 **프로퍼티처럼 값을 `할당`하는 형식으로 사용**하며 할당 시에 메소드가 호출됨
    ```jsx
    class Foo {
      constructor(arr = []) {
        this._arr = arr;
      }

      // getter: get 키워드 뒤에 오는 메소드 이름 firstElem은 클래스 필드 이름처럼 사용된다.
      get firstElem() {
        // getter는 반드시 무언가를 반환하여야 한다.
        return this._arr.length ? this._arr[0] : null;
      }

      // setter: set 키워드 뒤에 오는 메소드 이름 firstElem은 클래스 필드 이름처럼 사용된다.
      set firstElem(elem) {
        // ...this._arr은 this._arr를 개별 요소로 분리한다
        this._arr = [elem, ...this._arr];
      }
    }

    const foo = new Foo([1, 2]);

    // 클래스 필드 lastElem에 값을 할당하면 setter가 호출된다.
    foo.firstElem = 100;

    console.log(foo.firstElem); // 100
    ```
  ##### [정적 메소드]
  - 클래스의 **정적(static) 메서드**를 정의할 때 `**static` 키워드\*\*를 사용함
  - 정적 메서드는 클래스의 인스턴스가 아닌 **클래스 이름으로 호출**함
  - 따라서 클래스의 인스턴스를 생성하지 않아도 호출할 수 있다.
    ```jsx
    class Foo {
      constructor(prop) {
        this.prop = prop;
      }

      static staticMethod() {
        /*
        정적 메소드는 this를 사용할 수 없다.
        정적 메소드 내부에서 this는 클래스의 인스턴스가 아닌 클래스 자신을 가리킨다.
        */
        return "staticMethod";
      }

      prototypeMethod() {
        return this.prop;
      }
    }

    // 정적 메소드는 클래스 이름으로 호출한다.
    console.log(Foo.staticMethod());

    const foo = new Foo(123);
    // 정적 메소드는 인스턴스로 호출할 수 없다.
    console.log(foo.staticMethod()); // Uncaught TypeError: foo.staticMethod is not a function
    ```
  ##### [상속]
  - 클래스의 상속과 **오버라이딩**은 `super`를 사용해서 수행할 수 있음
    - 오버라이딩 : 객체의 상속받은 부모의 메소드를 재정의하는 것
    ##### ES5
    ```jsx
    var AddSquare = function (arg1, arg2) {
      Add.call(this, arg1, arg2);
    };

    Object.assign(AddSquare.prototype, Add.prototype);

    AddSquare.prototype = {
      calc: function () {
        // 메소드는 생략될 수 없습니다.
        Add.prototype.calc.call(this);
      },
      calcSquare: function () {
        this.pow = Math.pow(this.arg1 + this.arg2, 2);
        return "(" + this.arg1 + "+" + this.arg2 + ")^2=" + this.pow;
      },
    };

    var numSquare = new AddSquare(5, 8);
    console.log(numSquare.calc()); // 5 + 8 = 13
    console.log(numSquare.calcSquare()); // (5 + 8) ^ 2 =169
    ```
    ##### ES6
    ```jsx
    class AddSquare extends Add {
      constructor(arg1, arg2) {
        super(arg1, arg2);
      }
      calc() {
        super.calc();
      }
      calcSquare() {
        this.pow = Math.pow(this.arg1 + this.arg2, 2);
        return "(" + this.arg1 + "+" + this.arg2 + ") ^ 2 =" + this.pow;
      }
    }

    var numSquare = new AddSquare(5, 8);
    console.log(numSquare.calc()); // 5 + 8 = 13
    console.log(numSquare.calcSquare()); // (5 + 8) ^ 2 = 169
    ```

##### 7) 가변 파라미터

- 함수 사용시 기본 파라미터와 가변 파라미터를 지정가능함.
- 기본 파라미터 : 기존과 동일함.
- **가변 파라미터 : 기본 파라미터 외의 넘어온 파라미터를 배열로 묶어서 받을 수 있음.**
  (가변적으로 추가되도록 할 수 있음.)

##### ES7 (2016)

##### [목록]

- 제곱 연산자 (\*\*) 등장 - Math.pow 외에 제곱을 표현하기 위한 연산자
- Array.prototype.includes() 메서드 등장 - 배열에 해당요소가 존재하는지 확인하는 메서드

##### 1) 제곱 연산자 (\*\*)

##### ES6↓

```jsx
// 예전에는 제곱을 표현하기 위해 Math 객체를 사용함
Math.pow(5, 3); // 125
```

##### ES7

```jsx
5 ** 3; // 125

// 제곱에 대한 복합대입연산자 추가
var i = 2;
i **= 3; // 8

var i = 5;
i **= 3; // 125
```

##### 2) `Array.includes` 배열에 해당 요소가 존재하는지 확인하는 메소드 등장

- `indexOf`와 비슷하지만 다른 부분 : `indexOf`는 `NaN`을 못찾지만, `includes`는 찾을 수 있음
  ```jsx
  // 배열에 해당 요소가 있는 지 확인
  [1, 2, 3].includes(1); // true
  [1, 2, 3].includes(1, 1); // false

  [NaN].includes(NaN); // true
  [NaN].indexOf(NaN) > -1; // false
  ```

##### ES8 (2017)

##### [목록]

- `Promise` 급의 중대한 변화인 `async`, `await`등이 발표됨
  - Promise와 같이 비동기 처리를 위한 키워드로, **Promise보다 간결하고 직관적임.**
- `Object` 객체의 심화된 메소드 등장
- 문자열 단순 편의기능 추가
- 매개변수 마지막에 콤마를 붙이는 것을 허용
- 공유된 메모리와 원자
  - SharedArrayBuffer 객체와 Atomics 객체를 사용한 메모리 공유가 가능해짐.
  ##### 1) `Object` 객체의 심화된 메소드 등장
  #### [Object.values()]
  - `Object.keys`에 대응되는 메서드로 **객체의 열거 가능한 속성 값들만 배열로** 만들어줌
    ```jsx
    let obj = {
      a: "aaa",
      b: "bbb",
    };
    Object.values(obj); // ['aaa', 'bbb']
    ```
  #### [Object.entries()]
  - `Object.keys`와 `Object.values`를 합쳐 놓은 메서드로 **열거 가능한 속성명과 속성값을 2차원 배열**로 만들어줌
    ```jsx
    let obj = {
      a: "aaa",
      b: "bbb",
    };
    Object.entries(obj); // [['a', 'aaa'], ['b', 'bbb']]
    ```
  #### 2) 문자열 단순 편의기능 추가
  #### [문자열.padStart(최종길이, 보충문자열)]
  - 문자열 앞 부분에 공백이나 글자를 넣을 수 있어 최종 길이로 만들어줌 (자리수를 맞춰줌)
  - 보충문자열을 설정하면 빈 칸에 그 문자열이 들어가고 (최종 길이를 채울 때까지 무한반복) 없으면 그냥 띄어쓰기들이 들어감
  - 기존 문자열 길이보다 최종 길이 값이 작을 경우 최종 길이를 무시하고 기존 문자열을 반환
  #### [문자열.padEnd(최종길이, 보충문자열)]
  - padStart와 같지만 문자열 뒷 부분에 공백이나 글자를 넣을 수 있음

#### ES9 (2018)

#### [목록]

- `ES2017`의 `Stage-3` 기능들이 대거 정식 스펙으로 추가됨
- Object rest, spread 등장
- Promise에 finally (Promise.prototype.finally) 등장
- Async iteration을 for-await-of 구문에서 사용 가능
- 정규 표현식 업데이트 됨

#### 1) Object rest, spread

- 가장 자주 쓰게 될 기능으로 객체 해체와 비슷함
- **배열을 해체하던 것처럼 객체를 해체 할 수 있음**
- 먼저 `rest`는 선택되지 않은 나머지 속성들을 모아주는 기능을 하며 rest를 할 때 값은 복사하고, 객체는 참조함
  ```jsx
  console.log(rest); // { b: 2, c: 3}
  const { d, g, ...rest2 } = { d: 4, e: { f: 6 }, g: 7, h: 8 };
  console.log(rest2); // { e: { f: 6 }, h: 8 } ( { f: 6 }은 복사가 아니라 참조)
  ```
- `spread`는 `Object.assign`과 비슷한 기능을 함
  - 값은 복사하고, 객체는 참조함
- 만약 같은 속성명이 있다면 뒤의 것이 앞의 것을 덮어씌움
  ```jsx
  const obj = { a: 1, b: 2, c: 3 };
  const spread = {
    a: 3,
    d: 4,
    ...obj,
  };
  console.log(spread); // { a: 1, b: 2, c: 3, d: 4 } (a: 3이 덮어씌워짐)
  const spread2 = {
    a: 2,
    c: 4,
    ...obj,
    a: 3,
    b: 5,
  };
  console.log(spread2); // { a: 3, b: 5, c: 3 }
  ```

#### 2) Promise finally ()

- Promise에 then과 catch 외에도 `finally`가 추가됨
- Promise : 성공, 실패 여부와 상관없이 무조건 실행되는 메소드
- finally : 뒤에 다시 then이나 catch를 붙일 수도 있고,
  스펙에 따르면 finally에서 return하는 프로미스는 resolve 값은 바꿀 수 없고,
  reject 값만 바꿀 수 있다함
  ```jsx
  fetch("http://example.com/endpoint")
    .then((result) => {})
    .catch((err) => {})
    .finally(() => {});
  ```

#### 3) Async iteration (For-of 구문)

- async 문법을 `생성기`랑 `for of 문`에서 사용 가능
- 생성기와 for of 문에서 사용가능할 수 있게 되면서 **반복적인 비동기 작업을 쉽게 처리할 수 있게 됨**
  ```jsx
  (async () => {
    const promises = ["1000", "2000", "3000"].map(
      (timer) =>
        new Promise((res, rej) => {
          setTimeout(() => res(timer), timer);
        })
    );
    for await (const result of promises) {
      console.log(result);
    }
  })();
  ```

#### 4) 정규 표현식 업데이트

- 정규표현식도 업데이트 됨 `**lookbehind`가 생기고, 캡쳐링 그룹에 이름을 정해줄 수 있음\*\*
- s 플래그가 추가되어 .(점)의 기능이 강화됨 이제는 `\n`도 매칭함
- 유니코드를 위한 u 플래그가 추가되어, 특정 유니코드를 정규표현식으로 표현 가능
- 캡쳐링 그룹에 이름도 붙여줄 수 있음 캡쳐링 그룹이란 정규 표현식에서 괄호로 묶어준 것들을 의미하는데 보통 괄호 순서대로 1번, 2번, 3번 이렇게 번호로 이름이 매겨지는 것을 이제 사용자가 직접 지정할 수 있음 이렇게 매겨진 이름은 결과의 groups 속성으로 접근할 수 있음
  ```jsx
  const result = /(?<blue>파랑)(?<red>빨강)/.exec("파랑빨강");
  result.groups.blue; // 파랑
  result.groups.red; // 빨강
  result.groups[1]; // 파랑
  result.groups[2]; // 빨강
  ```

---

> lookbehind

<aside>
📌 특정 문자열 뒤의 문자열을 찾는 기능으로, 지금까지 **자바스크립트 정규표현식**은                              특정 문자열 앞의 문자열만 찾을 수 있었으나 이제 뒤의 것까지 찾아줌
* 이를 위해 ?>=와 ?>! 심볼이 추가됨_

</aside>

---

#### ES10 (2019)

#### [목록]

- 최신 크롬,파이어폭스에서 사용가능한 5가지 기능이 추가됨
- Object.fromEntries
- trimStart() 와 trimEnd()
- flat() 과 flatMap()
- Symbol 객체의 Description 속성
- 선택적 catch 바인딩

#### 1) Object.fromEntries()

- 객체를 배열로 바꾸는 것은 ES2017 에서 `Object.entries()` 메소드로 가능
- 이 메소드는 객체를 인자로 받아 `[key, value]` 형태의 `배열`로 반환함
- 배열 말고 `Map`같은 것도 지원함

```jsx
const obj = { one: 1, two: 2, three: 3 };
console.log(Object.entries(obj));
// => [["one", 1], ["two", 2], ["three", 3]]
```

#### 2) trimStart() 와 trimEnd()

- `trimStart()` 와 `trimEnd()` 메소드는 기술적으로 `trimLeft() / trimRight()` 와 동일함
- trimStart() 와 trimLeft()는 왼쪽 공백을 지우고, trimEnd()와 trimRight()는 오른쪽 공백을 지움.
- 하위 호환성 (옛날부터 있었던 메서드를 지원)을 위해 추가 됨

```jsx
"    abc    ".trim(); // 'abc'
"    abc    ".trimStart(); // 'abc    '
"    abc    ".trimEnd(); // '    abc'
"    abc    ".trimRight(); // '    abc'
"    abc    ".trimLeft(); // 'abc    '
```

#### 3) flat() 과 flatMap()

- `flat()` 메소드는 **배열 내부의 하위 배열을 쉽게 합칠 수 있음**
- 선택적 인자를 받을 수 있고 이는 배열의 깊이를 의미하는 숫자로, 아무것도 전달하지 않으면 기본값으로 1이 사용됨
  ```jsx
  const arr = ["a", "b", ["c", "d"]];
  const flattened = arr.flat();
  console.log(flattened);
  // => ["a", "b", "c", "d"]
  //  이전에는 reduce() 나 concat()을 사용해야 했음
  const arr = ["a", "b", ["c", "d"]];
  const flattened = [].concat.apply([], arr);
  // or
  // const flattened =  [].concat(...arr); console.log(flattened);
  // => ["a", "b", "c", "d"]
  ```
- `flatMap()` 메소드는 `map()`과 `flat()` 을 하나로 결합한 것임
- 처음에는 전달된 함수의 결과값을 배열로 만들고 내부 배열과 결합시킴
  ```
  const arr = [4.25, 19.99, 25.5];
  console.log(arr.map(value => [Math.round(value)]));
  // => [[4], [20], [26]]
  console.log(arr.flatMap(value => [Math.round(value)]));
  // => [4, 20, 26]
  ```

#### 4) Symbol 객체의 Description 속성

- Symbol 을 만들때, **디버깅 용도로 `description` 속성을 추가할 수 있음 (read-only)**
  ```jsx
  let sym = Symbol("foo");
  console.log(sym.description);
  // => foo

  sym = Symbol();
  console.log(sym.description);
  // => undefined

  // create a global symbol
  sym = Symbol.for("bar");
  console.log(sym.description);
  // => bar
  ```

#### 5) 선택적 catch 바인딩

- try … catch 구문에서 **항상 `catch` 바인딩이 사용되는 것은 아님**
  ```jsx
  try {
    // 브라우저에서 지원하지 않는 기능 사용
  } catch {
    // 넘겨주는 값을 신경쓰지 않고 뭔가 수행
  }
  ```
- 위 코드에서 catch 바인딩은 사용되지 않음
- 하지만 SyntaxError 를 피하기 위해 명시해야 했음 작은 변화지만 위 코드처럼 사용할 수 있음

#### ES11 (2020)

#### [목록]

- matchAll
- BigInt
- Promise.allSettled
- globalThis
- 옵셔널 체이닝 (?.)
- Nullish 병합 연산자 (??)
- String.prototype.matchAll

#### 1) matchAll

- 문자열에서 일치하는 정규표현식을 `iterator` 형식으로 반환
- 또한 캡처링 그룹(소괄호로 감싸진 것)도 결과로 반환함 기존 `정규표현식.exec` 과 비슷
  ```jsx
  const matchAllResult = "11a22b".matchAll(/(\d)(\D)/g);
  matchAllResult.next(); // { value: ['1a', '1', 'a'], done: false }
  matchAllResult.next(); // { value: ['2b', '2', 'b'], done: false }
  matchAllResult.next(); // { value: undefined, done: true }
  ```

#### 2) BigInt

- 자바스크립트는 큰 숫자를 표현하는 데 문제가 있었음 `2^53-1(Number.MAX_SAFE_INTEGER)`보다 큰 숫자를 처리할 수가 없었는데 `BigInt` 객체가 도입되어서 처리할 수 있게 되었음 숫자 뒤에 `n`을 붙임
- 단, `BigInt`끼리 계산하지 않으면 에러가 발생함 또한 Big`"Int"`이기 때문에 소수점은 표현하지 못하며 그리고 숫자와도 같지 않음 (`1n !== 1`)
- 그러나 `1n == 1`이니 새로운 타입이 생겼다고 봐도되며 그런데 또 일반 숫자와 크기 비교 & 정렬 가능
  ```jsx
  1n + 1n; // 2n
  typeof 1n; // bigint
  ```

#### 3) Promise.allSettled

- 기존 프로미스는 여러 프로미스 중 하나만 실패해도 catch로 이동하였지만 `allSettled` 은 개별적으로 성공 여부를 알려줌
  ```jsx
  Promise.allSettled([upload(), upload(), upload()]).then((result) => {
    console.log(result[0]); // { status: 'fulfilled', value: 'ok' }
    console.log(result[1]); // { status: 'rejected', reason: 'too big' }
    console.log(result[2]); // { status: 'fulfilled', value: 'ok' }
  });
  ```

#### 4) globalThis

- 예전에는 브라우저의 전역객체는 window였고 Node.js의 전역객체는 global이었음
- 둘이 달라서 분기처리를 해줘야 했던 경우가 많았는데 이제는 `globalThis`라는 것으로 통일됨 물론 기존 window나 global도 존재함
  ```jsx
  // 브라우저
  globalThis === window; // true;

  // Node.js
  globalThis === global; // true
  ```

#### 5) 옵셔널 체이닝

- `?.` 연산자를 사용하면 지저분한 방어 로직이나 유틸리티 라이브러리 없이 안전하고 깔끔하게 속성값에 접근할 수 있음
- 객체의 속성을 접근할 때 . 연산자 대신에 `?.` 연산자를 사용하면, 해당 객체가 nullish 즉, `undefined`나 `null`인 경우에 TypeError 대신에 `undefined`를 얻게 됨
  ```jsx
  // 기존
  console.log(a && a.b && a.b.c);

  // 옵셔널 체이닝 도입
  console.log(a?.b?.c);
  ```

#### 6) nullish coalescing

- 기존에는 삼항연산자나 기본값연산자(||) 보호연산자(&&)에서 조건문 부분에 null이나 undefined외에도 0, ’’, NaN, false 등은 거짓으로 처리되었음
- 이제 널 병합 연산자(`??`)를 사용하면 null과 undefined인 경우에만 거짓으로 처리됨
  ```jsx
  "" || "test"; // 'test';
  "" ?? "test"; // ''
  null || "test"; // 'test'
  null ?? "test"; // 'test'
  false ?? "test"; // false
  ```

#### ES12 (2021)

#### [목록]

- replaceAll
- Promise.any
- 논리 할당 연산자
- 숫자 구분 기호
- Intl.DateTimeFormat

#### 1) replaceAll

- 문자열을 한 번에 여러 개 바꿀 수 있는 편의 기능이 추가됨
  ```jsx
  "a,bb,ccc".replace(/,/g, " "); // 'a bb ccc'

  // replaceAll
  "a,bb,ccc".replaceAll(",", " "); // 'a bb ccc'
  ```

#### 2) Promise.any

- iterable한 Promise들을 인자로 받아 첫 번째로 해결된 Promise가 생기면 단락되고 값을 반환함
- `Promise.any`메서드는 입력된 Promise들 중 하나라도 성공하면 에러가 발생하지 않고 첫 번째로 성공한 promise의 값을 반환하지만 입력된 Promise들이 모두 실패하면 에러를 출력함
  ```jsx
  try {
    const first = await Promise.any(promises);
    // Promise 중 하나라도 성공한 경우
  } catch (error) {
    // 모든 Promise가 실패한 경우
  }

  // async/await을 사용하지 않은 경우
  Promise.any(promises).then(
    (first) => {
      // Promise 중 하나라도 성공한 경우
    },
    (error) => {
      // 모든 Promise가 실패한 경우
    }
  );
  ```

#### 3) 논리 할당 연산자

- 세 가지 논리 연산자가 할당 기능이 더해진 연산자
- `+=`, `=`와 같이 왼쪽의 피연산자를 오른쪽의 피연산자와 연산 후 다시 왼쪽의 피 연산자에게 대입하는 문법
- 최근 타입스크립트 4.0에 새롭게 추가된 기능인데 자바스크립트에서도 새롭게 추가됨
  ```jsx
  // before
  obj.prop = obj.prop || foo(); // obj.prop이 잘못된 값일 경우 할당
  obj.prop = obj.prop && foo(); // obj.prop이 올바른 값일 경우 할당
  obj.prop = obj.prop ?? foo(); // obj.prop이 null이나 undefined일 경우 할당

  // after
  obj.prop ||= foo();
  obj.prop &&= foo();
  obj.prop ??= foo();
  ```

#### 4) 숫자 구분 기호

- 숫자 구분 기호는 `_`을 사용해 숫자를 시각적으로 더 읽기 쉽게 만들어줌
- 숫자 리터럴의 가독성을 향상시키는 데 도움
  ```jsx
  // before
  10000000000; // 100억

  // after
  10_000_000_000; // 100억

  console.log(10_000_000_000); // 10000000000
  ```

### 참고 자료

- 자바스크립트 언어 자료 [https://developer.mozilla.org/ko/docs/Web/JavaScript/Language_Resources](https://developer.mozilla.org/ko/docs/Web/JavaScript/Language_Resources)
- 웹 프로그래밍 튜토리얼
  [https://poiemaweb.com/](https://poiemaweb.com/)
- ES2021/ ES12 New Features
  [https://backbencher.dev/articles/javascript-es2021-new-features](https://backbencher.dev/articles/javascript-es2021-new-features)
- ECMAScript 역사
  [https://wangchunsik.tistory.com/13](https://wangchunsik.tistory.com/13)
- Babel - ECMAScript 버전 별 확인
  [https://babeljs.io/docs/en/plugins-list](https://babeljs.io/docs/en/plugins-list)
- ES 버전 정리 참고
  - 각 버전 정리 및 버전별 특징 : [https://medium.com/sjk5766/ecma-script-es-%EC%A0%95%EB%A6%AC%EC%99%80-%EB%B2%84%EC%A0%84%EB%B3%84-%ED%8A%B9%EC%A7%95-77715f696dcb](https://medium.com/sjk5766/ecma-script-es-%EC%A0%95%EB%A6%AC%EC%99%80-%EB%B2%84%EC%A0%84%EB%B3%84-%ED%8A%B9%EC%A7%95-77715f696dcb)
  - ES5: [https://k39335.tistory.com/m/81](https://k39335.tistory.com/m/81)
  - ES6 : [https://velog.io/@syoung125/개념공부-1.-JavascriptES6란-ES7과-차이점](https://velog.io/@syoung125/%EA%B0%9C%EB%85%90%EA%B3%B5%EB%B6%80-1.-JavascriptES6%EB%9E%80-ES7%EA%B3%BC-%EC%B0%A8%EC%9D%B4%EC%A0%90)
  - ES7,8 : [https://lts0606.tistory.com/466](https://lts0606.tistory.com/466)
  - ES9 : [https://a-tothe-z.tistory.com/m/15](https://a-tothe-z.tistory.com/m/15)
  - ES11 : [https://john015.netlify.app/what-is-new-in-es-11](https://john015.netlify.app/what-is-new-in-es-11)
  - ES12 : [https://blog.woolta.com/categories/3/posts/207](https://blog.woolta.com/categories/3/posts/207)
- ES 크로스 브라우징 버전 확인
  - ES 버전 별 정리 표 : [http://kangax.github.io/compat-table/es6/](http://kangax.github.io/compat-table/es6/)
  - CSS, JS 등 버전 확인 : [https://caniuse.com/](https://caniuse.com/)
