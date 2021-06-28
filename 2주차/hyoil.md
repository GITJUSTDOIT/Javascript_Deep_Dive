# 모던 자바스크립트 Deep Dive 2주차 정리
## 12. 함수
---
## 12.4 함수 정의
| 함수 정의 형식 | 예시 |
| :--- | :--- |
|함수선언문| function add(x, y) { return x+y;} |
|함수표현식| var add = function(x, y) { return x+y; } |
|Function 생성자 함수| var add = new function('x', 'y', 'return x+y'); |
|화살표 함수(ES6)| var add (x,y) => x+y; | 

## 12.4.1~2 함수 선언문과 표현식
```javascript
// 자바스크립트엔진은 함수 선언문의 함수 이름으로 식별자를 암묵적 생성하고 생성된 함수 객체를 할당한다.
function sub(x, y) {
    return x - y;
};

console.log(sub(7, 5)); // 2
// 함수는 함수 이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출한다.
var add = function addFun(x, y) {
    return x + y;
};

console.log(add(2,5)); // 7
```
* 함수 선언문과 함수 표현식은 유사하게 동작하는 것으로 보이나 동일하게 동작하지 않는다.
* 함수 선언문은 "표현식이 아닌 문"이고 함수 표현식은 "표현식 문"이다.

## 12.4.3 함수 생성 시점과 함수 호이스팅
```javascript
console.log(add(5, 6)); // 11
console.log(sub(6, 5)); // typeError: sub is not a function
// 함수 선언문
function add(x, y) {
    return x + y;
}
// 함수 표현식
var sub = function (x, y) {
    return x - y;
}

/*자바스크립트에서 모든 선언문은 런타임 이전에 자바스크립트 엔진에 의해 먼저 실행된다.
즉 함수 선언문으로 함수를 정의 하면 런타임 이전에 함수객체가 먼저 생성된다.
그리고 동일한 이름으로 식별자를 암묵적으로 생성한다.*/
/*함수 호이스팅은 함수를 호출하기 전에 반드시 함수를 선언해야 한다는 당연한규칙을 무시함으로
함수 선언문 대신 함수 표현식 사용을 권장한다.*/
```
* 위처럼 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 함수 호이스팅이라 한다.
## 12.5 함수 호출
```javascript
// 인수를 적게 넘겨 줄 경우
// 인수가 부족 할 경우 에러가 발생하지 않고 할당되지 않는 매개변수는 undefined로 할당
function add(x, y) {
    return x + y;
}
console.log(add(2));// NaN

// 인수를 많이 넘겨 줄 경우
// 매겨변수보다 인수가 더 많은 경우 초과된 인수는 무시된다.
// But, 인수는 그냥 버려지는 것이 아니라 모든 인수는 암묵적으로 arguments 객체의 프로퍼티로 보관
function add2(x, y) {
    return x + y;
}
consol.log(add2(2, 5, 10)); // 7
```
## 12.5.4 반환문
```javascript
function foo() {
    return;
}
console.log(foo()) // undefined

function foo2() {

}
console.log(foo2()); // undefined

function foo3() {
    return
    x+y;
}
consolelog(foo3()); // undefined
// return문 과 반환값 사이에 줄 바꿈이 존재할 경우 return 옆에 세미콜론이 추가 된다.
```
## 12.7 즉시 실행 함수
```javascript
// 함수 정의와 동시에 즉시 호출 되는 함수로 단 한번만 호출된다. 보통 익명함수로 생성
(function () {
    var a = 3;
    var b = 5;
    return a * b;
}());
```

## 13. 스코프
* 모든 식별자(변수이름, 함수이름, 클래스이름 등)는 선언된 위치에 의해 다른코드가 자신을 참조하는 유효범위가 정해진다.
---
## 13.4.1 함수 레벨 스코프
```javascript
/* C나 JAVA 등은 대부부분 모든 코드 블록(if, for, while, try/catch 등)이 지역 스코프를 만든다 이러한 특성을 블록 레벨 스코프라고한다
하지만 var키워드로 선언된 변수는 오로지 함수의 코드블록(함수 몸체)만을 지역 스코프로 인정한다. 이러한 특성을 함수레벨 스코프라 한다.*/
var x = 1;
let y = 1;
if(true) {
    var x = 10;
    let y = 20;
    
    console.log(x); // 10
    console.log(y); // 20
}
console.log(x); // 10
console.log(y); // 1
```
## 13.5 렉시컬 스코프
```javascript
var x = 1;

function foo() {
    var x = 10;
    bar();
}

function bar() {
    console.log(x);
}

foo(); // 1
bar(); // 1
/*자바스크립트는 렉시컬 스코프를 따르므로 함수를 어디서 호출했는지가 아니라
함수를 어디서 정의했는지에 따라 상위 스코프를 결정한다. 즉, 함수의 상위 스코프는
언제나 자신이 정의된 스코프다.*/
```