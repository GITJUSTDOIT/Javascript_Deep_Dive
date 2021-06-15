# 모던 자바스크립트 Deep Dive 1주차 정리

## 1. 변수 선언
---
```javascript
/* var 키워드는 변수이름 name을 등록하고 암묵적으로 undefined를 할당해 초기화 한다.
(선언과 초기화 단계가 동시에 일어난다)*/
var name;
```
```javascript
/*처음 console.log( score )에서 참조에러가 발생하지 않는 이유는 
JavaScript에서 모든 선언문은 런타임(순차적 실행) 이전 단계에서 먼저 실행되기 때문이다.*/
console.log( score ); // undefined

var score;
score = 80;
console.log( score ); // 80
``` 
``` javascript
/*javascript는 변수 선언과 값의 하나의 문으로 단축 표현해도 변수 선언과 값의 할당을 2개의 문으로 나누어 각각 실행한다. */
var score = 80;
```
## 2. 변수 네이밍 규칙
---
* 특수문자를 제외한 문자, 숫자, 언더스코어(_), 달러기호($)를 포함할 수 있다.
* 특수문자를 제외한 문자, 언더스코어(_), 달러 기호($)로 시작해야 한다. 숫자로는 시작 할 수 없다.
* 예약어는 식별자로 사용할 수 없다.(true, case, class, typeof 등)
* JavaScript는 대소문자를 구분한다.
## 3. 데이터 타입
---
| 구분 | 데이터 타입 | 설명 |
| :--- | :--- | :---|
| 원시타입 | 숫자(number) 타입 | 숫자, 정수와 실수 구분 없이 하나의 숫자 타입만 존재|
| 원시타입 | 문자열(string) 타입 | 문자열|
| 원시타입 | 불리언(boolean) 타입 | 논리적 참(true)과 거짓(false) |
| 원시타입 | undefined 타입 | var 키워드로 선언된 변수에 암묵적으로 할당되는 값|
| 원시타입 | null 타입 | 값이 없다는 것을 의도적으로 명시할 때 사용하는 값 |
| 원시타입 | 심벌(symbol 타입) ES6에서 추가된 7번째 타입 |
| 객체타입 | | 객체, 함수, 배열 등 |

`number 타입`
```javascript
// 숫자 타입은 모두 실수로 처리된다.
console.log( 1 === 1.0 ); // true
console.log( 4 / 2 ); // 2(정수 처럼 보여도 사실은 실수)
console.log( 3 / 2 ); // 1.5
```
`string 타입`
```javascript
// 문자열 타입은  작은따옴표(' '), 큰따옴표(" "), 백틱(` `)으로 감싼다
// 자바스크립트에서는 보통 작은따옴표를 사용한다.
var string;
string = '문자열'; // 작은따옴표
string = "문자열"; // 큰따옴표
string = `문자열`; // 백틱(ES6부터 지원)
```
`boolean 타입`
```javascript
// true, false의 값만 존재
var foo = true;
console.log( foo ); // true

foo = false;
console.log( foo ); // false
```
`undefined 타입`
```javascript
// 변수 선언과 초기화가 같이 일어날때 
var foo;
console.log( foo ); // undefined
```
`null 타입`
```html
<!-- 자바스크립트는 대소문자를 구별하므로 null은 Null, NULL 등과 다르다.-->
<!DOCTYPE html>
<html>
<body>
    <script>
        var element = document.querySelector( '.myClass' );

        // HTML 문서에 myClass 클래스를 갖는 요소가 없다면 null을 반환한다.
        console.log( element ); // null
    </script>
</body>
</html>
```
`symbol 타입`
```javascript
// symbol key에는 keyName이라는 설명이 붙는다.
var key = symbol( 'keyName' );
console.log(typeof key); // symbol 타입

var id1 = Symbol("id");
var id2 = Symbol("id");

/*심볼은 유일성이 보장되는 자료형이기 때문에, 설명이 동일한 심볼을 여러 개 만들어도 각 심볼값은 다르다.
 심볼에 붙이는 설명(심볼 이름)은 어떤 것에도 영향을 주지 않는 이름표 역할만을 합니다*/
alert(id1 == id2); // false

// 이름이 충돌할 위험이 없는 유일한 값인 심벌을 프로퍼티 키로 사용
var obj = {};

obj[key] = 'val';
console.log( obj[key] ); // val
```
> symbol 타입은 33장에서 자세히 살펴본다고 한다.

`object 타입`   
```javascript
// 자바스크립트는 위의 6가지 타입을 제외하고 모두 객체 타입이다.
var obj = {};

obj.id = 'ds8080';
obj.name = '신효일';
```
> 객체 타입은 11장에서 자세히 살펴본다고 한다.

## 4. 템플릿 리터럴
---
1. ES6부터 템플릿 리터럴이라고 하는 새로운 문자열 표기법이 도입되었다.   
2. 템플릿 리터럴은 일반 문자열과 비슷해 보이지만 작은따옴표('') OR 큰따옴표("") 대신 백틱(``)을 사용해 표현한다.   

`멀티라인 문자열`
```javascript
/* 일반 문자열 내에서는 줄바꿈(개행)이 허용 되지 않는다.
그래서 일반 문자열 내에서 줄바꿈 등의 공백을 표현하기 위해 이스케이프시퀀스를 사용한다.*/
var str = 'Hello
world.'; // syntaxError: Invalid or unexpected token
```
```javascript
// 작은 따옴표( '' )나 큰 따옴표( "" ) 사용 시
var template = '<ul>\n\t<li><a href="#">Home</a></li>\n</ul>';
console.log(template);

// 결과
<ul>
	<li><a href="#">Home</a></li>
</ul>

// 백틱( `` ) 사용 시
var template2 = `<ul>
    <li><a href="#">Home</a></li>
</ul>`;
console.log(template2);

// 결과
<ul>
    <li><a href="#">Home</a></li>
</ul>

// 백틱(``)을 사용 시 따옴표를 사용할 때 보다 상대적으로 가독성도 좋고 사용하기; 편하다.
```
`표현식 삽입`
```javascript
var first = 'Hyo-il';
var last = 'Shin';

// 작은 따옴표( '' )나 큰 따옴표( "" ) 사용 시
console.log('My name is ' + first + ` ` + last + '.'); // My name is Hyo-il Shin.

// 백틱( `` ) 사용 시
console.log(`My name is ${first} ${last}.` ); // My name is Hyo-il Shin.

// 백틱을 사용할 때 표현식을 삽입하려면 ${}으로 표현식을 감싼다.
// 표현식의 평가 결과가 문자열이 아니더라도 문자열로 타입이 강제로 변환된다. 
```
## 5. 동등/일치 비교 연산자
---
|비교연산자|의미|사례|설명|
| :---: | :--- | :--- |:---|
|==|동등비교|x == y|x와y의 값이 같음|
|===|일치비교|x === y|x와y의 값과 타입이 같음|
|!=|부동등비교|x != y|x와y의 값이 다름|
|!==|부일치비교|x !== y|x와y의 값과 타입이 다름|

## 6. typeof 연산자
```javascript
typeof '' // -> "string"
typeof 1 // -> "number"
typeof NaN // -> "number"
typeof true // -> "boolean"
typeof undefined // -> "undefined"
typeof Symbol() // -> "symbol"
typeof null // -> "object"
typeof [] // -> "object"
typeof {} // -> "object"
typeof new Date() // -> "object"
typeof /test/gi // -> "bject"
typeof function () {} // -> "function"

/* typeof 연산자로 null 값을 연산해 보면 "null"이 아닌 "object"를 반환하는데
이것은 자바스크립트의 첫 번째 버전의 버그다. 기존 코드에 영향을 줄 수 있기 때문에 아직 수정이 되지 못했자.*/
// null타입인지 확인할 때는 일치 연산자(===)을 사용 하자
var foo = null;

typeof foo === null; // false
foo === null; // true
```
## 7. break문, continue문
---
```
break : 반복문(for, for...in, for...of, while, do...while) 또는 switch문의 코드 블록을 탈출한다.
continue : 반복문의 코드 블록 실행을 현 시점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다.
```