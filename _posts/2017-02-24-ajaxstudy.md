---
layout: post
title: "Pure Js Ajax 스터디"
description: "자바스크립트로 ajax api와 구동원리를 정리함"
date: 2017-02-27
tags: [js, ajax]
comments: true
share: true
---

![ajax](http://jijong.github.io/images/img_ajax.png)

# Ajax

***

jQuery api에서 제공하는 편리한 $.ajax() 메서드가 있지만 순수 자바스크립트 `XMLHttpRequest` 객체를 학습하기 위하여 포스트 하였다.
근데 실무에서는 아무래도 $.ajax() 메서드를 쓸것 같긴 하다.

## 목차

* [Ajax란?](#)
* [Ajax의 원리](#)
    * [순서](#)
    * [장점](#)
    * [XMLHttpRequest 객체 생성하기](#)
* [Ajax 서버 요청](#)
    * [GET방식과 POST방식 차이](#)
    * [GET Requests](#)
    * [POST Requests](#)
    * [서버 상의 파일 주소](#)
    * [비동기식 - True or False](#)
    * [Async = true](#)
    * [Async = false](#)
    * [XMLRequest readyState 값](#)
    * [XMLRequest Status 값](#)
* [Ajax 서버 응답](#)
    * [reponseText 속성](#)
    * [reponseXML 속성](#)
* [Ajax 이벤트](#)
    * [onreadystatechange 이벤트](#)
    * [Callback 함수 사용하기](#)
* [Ajax 데이터베이스](#)
    * [showCustomer() 함수](#)
    * [Ajax 서버 페이지](#)
* [Ajax 예제](#)
    * [XML의 응용 프로그램](*)
* 참고 링크
    
## Ajax란?

Ajax는 Asynchronous Javascript And Xml의 약자로, 비동기식 자바스크립트와 확장 마크업 언어를 뜻한다.
Ajax를 이용함으로써, 데이터 이용량은 줄이고, 페이지를 새로고침하는 시간도 줄어들었다.

## Ajax의 원리

### 순서

![ajax상호작용](http://jijong.github.io/images/img_ajax_load.png)

1. 클라이언트에서 `XMLHttpRequest` 객체를 생성하여 서버로 보낸다.
2. 서버에서 메시지를 받으면 해당 정보를 다시 브라우저로 보낸다.
3. 클라이언트가 서버로부터 응답을 받으면 해당 정보를 특정 영역에 뿌려준다.

Ajax를 사용함에 있어 가장 기본은 `XMLHttpRequest` 객체이다. 이 객체는 서버로부터 데이터를 전송받을 때 사용되는 객체이다.

> XMLHttpRequest 란?<br /><br />
XMLHttpRequest는 본래 ActiveX의 구성요소 중 하나로 IE5에서 처음 구현되었다. 최근에 Firefox, Safari, Opera등의 브라우저에서 XMLHttpRequest를 지원하면서 AJAX의 기반기술이 되었다. 하지만 여전히 XMLHttpRequest는 W3C 표준이 아님을 기억해야 한다. W3C의 표준안은 DOM Level3 Load and Save라는 이름의 스펙으로 존재한다. 하지만 DOM Level3는 현재 대부분의 브라우저에서 지원하지 않는다.

### 장점

- 페이지를 다시 불러오지 않고도 페이지를 다시 불러올 수 있다.
- 페이지를 불러오고 나서 서버에 데이터를 요청할 수 있다.
- 페이지를 불러오고 나서 서버에서 데이터를 받을 수 있다.
- 화면 뒷단에서 서버에 데이터를 보낼 수 있다.

### XMLHttpRequest 객체 생성하기

```javascript
var xhttp;
if(window.XMLHttpRequest){
    xhttp = new XMLHttpRequest();
}else{
    // IE5, IE6 일때
    xhttp = new ActiveXObject("Microsoft.XMLHTTP");
}
```

## Ajax 서버 요청

서버로 요청할때는 `XMLHttpRequest` 객체에서 제공하는 api 인 open(), send() 메소드를 사용한다. 

| 메소드 | 설명 |
| :----- | :---- |
| open(method, url, async) | 요청 타입을 정한다. <br />method: 요청 타입: GET 또는 POST<br /> url: 서버 (파일) 위치<br /> async: true (비동기식) 또는 false (동기식) |
| send() | 서버로 요청을 보낸다 (GET방식에서 사용) |
| send(string) | 서버로 요청을 보낸다 (POST방식에서 사용) | 

### GET방식과 POST방식 차이

GET은 POST보다 단순하고 빠르며 대부분의 경우에 사용할 수 있다.<br />
하지만 아래 경우에는 꼭 POST 방식으로 써야한다.

- A cached file is not an option (서버에 있는 파일이나 데이터베이스를 업데이트 하는 경우)
- 서버로 많은 양의 데이터 전송이 필요한 경우 (GET방식은 전송할 데이터 사이즈 제한이 있으나 POST방식은 사이즈 제한이 없다.)
- (unknown characters를 포함할 수 있는) 사용자 input을 서버로 전송할 때, POST 방식이 보안상 GET방식보다 좋다.

### GET Requests

```javascript
xhttp.open('GET', 'dome_get.asp', true);
xhttp.send();
```

위 소스는 이미 캐시댄 결과를 볼 수도 있다. 그런 경우를 피하려면, 유니크 ID를 URL에 삽입해야 한다.

```javascript
xhttp.open('GET', 'dome_get.asp?t=' + Math.random(), true);
xhttp.send();
```

GET 방식으로 요청을 보내고 싶으면, 정보를 URL에 입력해주면 된다.

```javascript
xhttp.open('GET', 'dome_get2.asp?fname=Henry&lname=Ford', true);
xhttp.send();
```

### POST Requests

```javascript
xhttp.open('POST', 'demo_post.asp', true);
xhttp.send();
```

HTML 형식으로 POST 요청을 하려면, setRequestHeader()를 이용하여 HTTP 헤더 정보를 넣어주면 된다.
그리고 send() 메서드에 보내려는 데이터정보를 넣어주면 된다.

```javascript
xhttp.open('POST', 'demo_post.asp', true);
xhttp.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
xhttp.send('fname=Henry&lname=Ford');
```

### 서버 상의 파일 주소

open() 메서드의 url 파라미터는 서버에 위치한 파일의 주소이다.

```javascript
xhttp.open('GET', 'ajax_test.asp', true);
```

여기서 말하는 파일은 .txt, .xml 파일처럼 평범한 파일들, 또는 .asp, .php와 같은 서버스크립팅 파일이다.
(서버스크립트 파일들은 서버에서 응답을 보내기 전에 특정 일을 수행할 수 있다.)

### 비동기식 - True or False

ajax를 사용하려면 3번째 파라미터는 무조건 `true` 여야 한다

```javascript
xhttp.open('GET', 'ajax_test.asp', true);
```

### Async = true

```javascript
xhttp.onreadystatechange = function(){
    if(xhttp.readyState == 4 && xhttp.status == 200){
        document.getElementById('demo').innerHTML = xhttp.responseText;
    }
};
xhttp.open('GET', 'ajax_info.txt', true);
xhttp.send();
```

### Async = false

```javascript
xhttp.open('GET', 'ajax_test.asp', false);
```

async=false 로 사용하게 되면 더이상 ajax를 사용하지 않는 다는 선언이다. 이렇게 서버로 요청을 하게 되면 서버에서 응답이
오기 전까지 화면에서 아무것도 할 수 없는 상황이 발생한다.

```javascript
xhttp.open('GET', 'ajax_info.txt', false);
xhttp.send();
document.getElementById('demo').innerHTML = xhttp.responseText;
```

### XMLRequest readyState 값 

| 코드 | 상태 | 설명 |
| :--- | :---- | :--- |
| 0 | UNINITIALZED | XMLHttpRequest 객체를 생성하였지만, 초기화되지 않았다. open()메서드 실행 전
| 1 | LOADING | XMLHttpRequest 객체를 생성하였고, open() 메서드를 수행하였지만 send() 메서드를 수행하지 않은 상태
| 2 | LOADED | Send()메서드를 수행하였지만, 서버가 처리를 준비하고 있는 상태
| 3 | INTERACTIVE | 처리를 완료하지 않았지만, 진행 중인 상태
| 4 | COMPLETED | 처리를 완료한 상태

### XMLRequest Status 값

| Number | Description |
| :------ | :----------- |
| 100 | Continue |  
| 101 | Switching protocols | 
| 200 | OK |
| 201 | Created |
| 202 | Accepted | 
| 203 | Non-Authoritative<br />Information |
| 204 | No Content |
| 205 | Reset Content |
| 206 | Partial Content |
| 300 | Multiple Choices |
| 301 | Moved Permanently |
| 302 | Found  |
| 303 | See Other |
| 304  | Not Modified |
| 305  | Use Proxy  |
| 307   | Temporary Redirect  |
| 400   | Bad Request |
| 401   | Unauthorized |
| 402   | Payment Required |
| 403   | Forbidden |
| 404   | Not Found |
| 405   | Method Not Allowed |
| 406   | Not Acceptable  |
| 407   | Proxy Authentication Required  |
| 408   | Request Timeout  |
| 409   | Conflict  |
| 410   | Gone   |
| 411    | Length Required    |
| 412     | Precondition Failed |
| 413  | Request Entity Too Large |
| 414     | Request-URI Too Long |
| 415  | Unsupported Media Type |
| 416     | Requested Range Not Suitable |
| 417     | Expectation Failed |
| 500 | Internal Server Error  |
| 501 | Not Implemented|
| 502 | Bad Gateway  |
| 503  | Service Unavailable  |
| 504 | Gateway Timeout  |
| 505 | HTTP Version Not Supported |

## Ajax 서버 응답

서버로부터 응답을 받기 위해서는 `XMLHttpRequest` 객체의 `reponseText` 또는 `reponseXML` 속성을 사용한다.

| 속성 | 설명 |
| :--- | :---- |
| responseText | 응답 데이터를 string으로 받는다. |
| responseXML | 응답 데이터를 XML로 받는다.

### reponseText 속성

```javascript
document.getElementById('demo').innerHTLM = xhttp.responseText;
```

### responseXML 속성

cd_catalog.xml이 있다고 가정했을 때, 파일을 요청하고 응답으로온 데이터 파싱하기

```javascript
xmlDoc = xhttp.responseXML;
txt = '';
x = xmlDoc.getElementsByTagName('artist');
for(i = 0; i < x.length; i++){
    txt += x[i].childNodes[0].nodeValue + '<br />';
}
document.getElementById('demo').innerHTML = txt;
```

## Ajax 이벤트

### onreadystatechange 이벤트

`XMLHttpRequest` 객체는 상태정보를 가지고 있는데, `readyState` 속성이 그 값을 가지고 있다.
그리고 우리는 이 상태 정보를 보고 응답이 왔는지, 그 응답이 정상적으로 왔는지 확인할 수 있다.
이 `readyState` 가 변할 때마다 항상 발생하는 이벤트가 있는데 그것이 바로 `onreadystatechange` 이벤트 이다.
`XMLHttpRequest` 객체의 중요한 세 가지 속성은 아래와 같다.

| 속성 | 설명 |
| :--- | :--- |
| onreadystatechange | readyState 속성값이 변할 때마다 자동으로 호출될 함수 또는 함수명을 저장 |
| readyState | XMLHttpRequest 객체의 상태를 가지고 있고, 0 에서 4 의 값을 가진다.<br />0: 요청이 초기화되지 않음. <br />1: 서버와 연결됨. <br />2: 요청이 받아들여짐<br /> 3: 요청이 진행중<br />4: 요청완료 및 응답완료
| status | 200: 정상<br />404: 페이지를 찾을 수 없음.

`onreadystatechange` 이벤트가 발생하고 `readyState`가 4이며 `status`가 200이면 정상적으로 요청이 처리되어 응답이 온 경우이다.

```javascript
function loadDoc(){
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function(){
        if(xhttp.readyState == 4 && xhttp.status == 200){
            document.getElementById('demo').innerHTML = xhttp.responseText;
        }
    };
}
```

> onreadystatechange 이벤트는 한번의 요청을 할 때 총 5번 발생한다. (readyState가 0에서 4까지 바뀌므로)

### Callback 함수 사용하기

callback 함수는 다른 함수의 파라미터로 넘겨지는 함수를 말한다.
만약 웹사이트에 하나 이상의 Ajax 작업이 있다면, 단 하나의 표준 함수를 만들어서 `XMLHttpRequest` 객체를 생성하고 각자의
Ajax 작업이 있을 때마다 이 표준함수에서 호출함으로써 코드를 단순화 할 수 있다.
표준함수는 각각의 Ajax 작업을 하는 함수를 파라미터로 넘겨받아 이를 처리하게 된다.

```javascript
function loadDoc(cFunc){
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function(){
        if(xhttp.readyState == 4 && xhttp.status == 200){
            cFunc(xhttp);
        }
    };
}
```

## Ajax 데이터베이스

### showCustomer() 함수 

사용자가 드랍다운 리스트에서 고객을 선택하면, `showCustomer()` 함수가 호출되어 실행된다. 이 함수는 `onchange` 이벤트
가 발생하면 호출되도록 되어있다.

```javascript
function showCustomer(str){
    var xhttp;
    if(str == ''){
        document.getElementById('txtHint').innerHTML = '';
        return;
    }
    xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function(){
        if(xhttp.readyState == 4 && xhttp.status == 200){
            document.getElementById('txtHint').innerHTML = xhttp.responseText;
        }
    };
    xhttp.open('GET', 'getcustomer.asp?q='+str, true);
    xhttp.send();
}
```

`showCustomer()` 함수는 아래와 같은 작업을 한다.
- customer가 선택이 되었는지 검사한다.
- `XMLHttpRequest` 객체를 생성한다.
- 서버로부터 응답을 받고나서 실행될 함수를 정의한다.
- 서버에 있는 파일로 요청을 보낸다.
- 요청을 보낼 때 파라미터 'q'와 드랍다운 리스트에서 읽어온 str을 URL에 추가했다.

### Ajax 서버 페이지

위 소스에서 사용된 서버페이지는 "getcustomer.asp" 이다.
서버 페이지 파일은 PHP, JSP와 같은 서버 언어로도 구현할 수 있다.
"getcustomer.asp"는 데이터베이스의 정보를 조회하고 읽어온 정보를 HTML 테이블에 넣는 기능을 한다.

```asp
<%
response.expires=-1
sql = "select * from customers where customeid="
sql = sql & "'" & request.querystring("q") & "'"

set conn = Server.CreateObject("ADODB.Connection")
conn.Provider = "Microsoft.Jet.OLEDB.4.0"
conn.Open(Server.Mappath("/datafolder/northwind.mdb"))
set rs = Server.CreateObject("ADODB.recordset")
rs.Open sql, conn

response.write("<table");
do until rs.EOF
    for each x in rs.Fields
        response.write("<tr><td><b>" & x.name & "</b></td>")
        response.write("<td>" & x.value & "</td></tr>")
    next
    rs.MoveNext
loop
response.write("</table>")
%>
```

1. 드랍다운 리스트에서 항목을 선택한다.
2. 항목이 선택되면 `onchange` 이벤트에 의해 showCustomer() 함수를 호출하여 Ajax 요청이 서버로 전송된다.
3. 서버에서 getcustomer.asp파일이 실행외 되고 이 파일은 DB를 조회해서 읽어온 정보를 html형태의 테이블을 만들어서
응답으로 보내준다.
4. 이 응답을 받은 html형식의 정보를 드랍다운 리스트 아래쪽에 뿌려준다.

## Ajax 예제

### XML의 응용 프로그램

이 예제에서는 `HTTP`, `DOM`, `Javascript XML`을 사용하여 일부 HTML 응용 프로그램을 보여준다.

```html
<html>
<head>
<style>
table, th, td {
  border: 1px solid black;
  border-collapse:collapse;
}
th, td {
  padding: 5px;
}
</style>
</head>
<body>

<table id="demo"></table>

<script>
function loadXMLDoc() {
  var xmlhttp = new XMLHttpRequest();
  xmlhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      myFunction(this);
    }
  };
  xmlhttp.open("GET", "cd_catalog.xml", true);
  xmlhttp.send();
}
function myFunction(xml) {
  var i;
  var xmlDoc = xml.responseXML;
  var table="<tr><th>Artist</th><th>Title</th></tr>";
  var x = xmlDoc.getElementsByTagName("CD");
  for (i = 0; i <x.length; i++) { 
    table += "<tr><td>" +
    x[i].getElementsByTagName("ARTIST")[0].childNodes[0].nodeValue +
    "</td><td>" +
    x[i].getElementsByTagName("TITLE")[0].childNodes[0].nodeValue +
    "</td></tr>";
  }
  document.getElementById("demo").innerHTML = table;
}
</script>

</body>
</html>
```

XML 파일은 [cd_catalog.xml](https://www.w3schools.com/js/cd_catalog.xml) 서 불러오며 <CD> 요소를 통해
HTML 테이블의 ARTIST, TITLE 요소를 뽑아온다.

```html
<!DOCTYPE html>
<html>
<body>

<div id='showCD'></div><br>
<input type="button" onclick="previous()" value="<<">
<input type="button" onclick="next()" value=">>">

<script>
var i = 0;
displayCD(i);

function displayCD(i) {
    var xmlhttp = new XMLHttpRequest();
    xmlhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            myFunction(this, i);
        }
    };
    xmlhttp.open("GET", "cd_catalog.xml", true);
    xmlhttp.send();
}

function myFunction(xml, i) {
    var xmlDoc = xml.responseXML; 
    x = xmlDoc.getElementsByTagName("CD");
    document.getElementById("showCD").innerHTML =
    "Artist: " +
    x[i].getElementsByTagName("ARTIST")[0].childNodes[0].nodeValue +
    "<br>Title: " +
    x[i].getElementsByTagName("TITLE")[0].childNodes[0].nodeValue +
    "<br>Year: " + 
    x[i].getElementsByTagName("YEAR")[0].childNodes[0].nodeValue;
}

function next() {
if (i < x.length-1) {
  i++;
  displayCD(i);
  }
}

function previous() {
if (i > 0) {
  i--;
  displayCD(i);
  }
}
</script>

</body>
</html>
```

<cd> 요소의 갯수를 반환하여 페이지화를 시킨 예제 이다.

## 참고 링크

- [w3cschool](https://www.w3schools.com/js/js_ajax_intro.asp)
- [Ajax 시작하기](http://blog.naver.com/stork838/220585220820)
- [XMLHttpRequest](http://cafe.naver.com/q69/116162) 

