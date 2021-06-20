# 12 함수

## 12.4.4 Function 생성자 함수

처음 알았는데 built in 함수라고 함.

[예제 12-13]
``` javascript
let add = new Function('x', 'y', 'return x + y'); // let add = Function('x', 'y', 'return x + y'); 으로 해도 됨
console.log(add(2, 5)); // 7
```

이런 방식은 일반적이지 않으며 바람직하지 않음.

## 12.5.2 인수 확인

타입스크립트를 써서 컴파일 시점에 부적절한 호출 방지

혹은

ES6에서 도입된 매개변수 기본값을 사용해서 인수 체크 및 초기화 가능

[예제 12-25]
``` javascript
let add = (a = 0, b = 0, c = 0) => a + b + c;

console.log(add(1, 2, 3));  // 6
console.log(add(1, 2));  // 3
console.log(add(1));  // 1
console.log(add());  // 0
```

## 12.7.1 즉시 실행 함수

IIFE, Immediately Invoked Function Expression

아래 형태가 가장 일반적인 형태임, 리턴 값을 받을 수 있고 파라미터 전달도 가능

[예제 12-42]
``` javascript
let res = (function () {
    let a = 3;
    let b = 5;
    return a * b;
}());

console.log(res);   // 15

res = (function (a, b) {
    return a * b;
}(3, 5));

console.log(res);   // 15
```

# 14장 전역 변수의 문제점

## 14.1.1 지역 변수의 생명 주기

[예제 14-02]

``` javascript
var x = 'global';

function foo() {
    consoel.log(x); // ??
    var x = 'local';
}

foo();
console.log(x); // global
```

출력은 undefined.
x는 foo() 함수 내부에서 선언과 동시에 undefined로 초기화됨. 전역 변수 x를 참조하지 않고 지역변수 x를 참조함.

## 14.1.2 전역 변수의 생명 주기

전역 객체 (global object)

> ... 전역 객체는 클라이언트 사이드 환경(브라우저)에서는 window, 서버 사이드 환경(Node.js)에서는 global 객체를 의미한다. 환경에 따라 전역 객체를 가리키는 다양한 식별자(window, self, this, frames, global)가 존재했으나 ES11에서 globalThis로 통일되었다.

# 15장 let, const 키워드와 블록 레벨 스코프

## 15.4 var vs. let vs. const

- ES6를 사용한다면 var 키워드는 사용하지 않는다.
- 재할당이 필요한 경우에 한정해 let 키워드를 사용한다. 이때 변수의 스코프는 최대한 좁게 만든다.
- 변경이 발생하지 않고 읽기 전용으로 사용하는(재할당이 필요 없는 상수) 원시 값과 객체에는 const 키워드를 사용한다. const 키워드는 재할당을 금지하므로 var, let 키워드보다 안전하다.

# 16장 프로퍼티 어트리뷰트

## 16.2 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

property attribute 확인

- Object.getOwnPropertyDescriptor
- Object.getOwnPropertyDescriptors

[예제 16-02]

``` javascript
const person = {
    name: 'Lee'
};

// 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 반환한다
console.log(Object.getOwnPropertyDescriptor(person, 'name'));
// { value: "Lee", writable: true, enumerable: true, configurable: true }
```

[예제 16-03]

``` javascript
const person = {
    name: 'Lee'
};

// 프로퍼티 동적 생성
person.age = 20;

// 모든 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환한다
console.log(Object.getOwnPropertyDescriptor(person));
/*
{
    name: { value: "Lee", writable: true, enumerable: true, configurable: true },
    age: { value: 20, writable: true, enumerable: true, configurable: true },
}
*/
```

### 16.3.2 접근자 프로퍼티

객체의 getter, setter 메소드\
get, set, enumerable, configurable을 가짐

[예제 16-06]

``` javascript
const person = {
    // 데이터 프로퍼티
    firstName: 'Jongfeel',
    lastName: 'Kim',

    // fullName은 접근자 함수로 구성된 접근자 프로터티다.
    // getter 함수
    get fullName() {
        return `${this.firstName} ${this.lastName}`
    },
    // setter 함수
    set fullName(name) {
        // 배열 디스트럭처링 할당: "31.1 배열 디스트럭처링 할당" 참고
        [this.firstName, this.lastName] = name.split(' ');
    }
};

// 데이터 프로퍼티를 통한 프로터티 값의 참조
console.log(person.firstName + ' ' + person.lastName); // Jongfeel Kim

// 접근자 프로퍼티를 통한 프로퍼티 값의 저장
// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
person.fullName = 'Heegun Lee';
console.log(person); // { firstName: "Heegun", lastName: "Lee" }

// 접근자 프로터티를 통한 프로터티 값의 참조
// 접근자 프로터티 fullName에 접근하면 getter 함수가 호출된다.
console.log(person.fullName); // Heegun Lee

// firstName은 데이터 프로퍼티다.
// 데이터 프로퍼티는 [[Value]], [[Writable]], [[Enumerable]], [[Configurable]]
// 프로터티 어트리뷰트를 갖는다.
let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
console.log(descriptor);
// { value: "Heegun", writable: true, enumerable: true, configurable: true }

// fullName은 접근자 프로퍼티다.
// 접근자 프로터티는 [[Get]], [[Set]], [[Enumerable]], [[Configurable]]
// 프로터티 어트리뷰트를 갖는다.
descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
console.log(descriptor);
// { get: f, set: F, enumerable: true, configurable: true }
```

## 16.4 프로퍼티 정의

Object.defineProperty

[예제 16-08]

``` javascript
const person = {};

// 데이터 프로퍼티 정의
Object.defineProperty(person, 'firstName', {
    value: 'Ungmo',
    writable: true,
    enumerable: true,
    configurable: true
});

Object.defineProperty(person, 'lastName', {
    value: 'Lee' 
});

let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
console.log('firstName', descriptor);
// firstName { value: "Ungmo", writable: true, enumerable: true, configurable: true }

// 디스크립터 객체의 프로퍼티를 누락시키면 undefined, false가 기본값이다.
descriptor = Object.getOwnPropertyDescriptor(person, 'lastName');
console.log('lastName', descriptor);
// lastName { value: "Lee", writable: false, enumerable: false, configurable: false }

// [[Enumerable]]의 값이 false인 경우
// 해당 프로퍼티는 for...in 문이나 Object.keys 등으로 열거할 수 없다.
// lastName 프로퍼티는 [[Enumerable]]의 값이 false이므로 열거되지 않는다.
console.log(Object.keys(person));   // ["firstName"]

// [[Writable]]의 값이 false인 경우 해당 프로퍼티의 [[Value]]의 값을 변경할 수 없다.
// lastName 프로퍼티는 [[Writable]]의 값이 false이므로 값을 변경할 수 없다.
// 이때 값을 변경하면 에러는 발생하지 않고 무시된다.
person.lastName = "Kim";

// [[Configurable]]의 값이 false인 경우 해당 프로퍼티를 삭제할 수 없다.
// lastName 프로퍼티는 [[Configurable]]의 값이 false이므로 삭제할 수 없다.
// 이때 프로퍼티를 삭제하면 에러는 발생하지 않고 무시된다.
delete person.lastName;

// [[Configurable]]의 값이 false인 경우 해당 프로퍼티를 재정의할 수 없다.
// Object.defineProperty(person, 'lastName', { enumerable: true });
// Uncaught TypeError: Cannot redefine property: lastName

descriptor = Object.getOwnPropertyDescriptor(person, 'lastName');
console.log('lastName', descriptor);
// lastName { value: "Lee", writable: false, enumerable: false, configurable: false }

// 접근자 프로퍼티 정의
Object.definePropety(person, 'fullName', {
    // getter 함수
    get() {
        return `${this.firstName} ${this.lastName}`;
    },
    // setter 함수
    set(name) {
        [this.firstName, this.lastName] = name.split(' ');
    },
    enumerable: true,
    configurable: true
});

descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
console.log('fullName', descriptor);
// fullName { get: f, set: f, enumerable: true, configurable: true }

person.fullName = "Heegun Lee";
console.log(person); // { firstName: "Heegun", lastName: "Lee" }
```

### 16.5.1 객체 확장 금지

Object.preventExtensions 메서드는 객체의 확장을 금지한다.

[예제 16-10]

``` javascript
const person = { name: 'Lee' };

// person 객체는 확장이 금지된 객체가 아니다.
console.log(Object.isExtensible(person)); // true

// person 객체의 확장을 금지하여 프로퍼티 추가를 금지한다.
Object.preventExtensions(person);

// person 객체는 확장이 금지된 객체다.
console.log(Object.isExtensible(person)); // false

// 프로퍼티 추가가 금지된다.
person.age = 20; // 무시. strict mode에서는 에러
console.log(person); // { name: "Lee" }

// 프로퍼티 추가는 금지되지만 삭제는 가능하다.
delete person.name;
console.log(person); // {}

// 프로퍼티 정의에 의한 프로퍼티 추가도 금지된다.
Object.defineProperty(person, 'age', { value: 20 });
// TypeError: Cannot define property age, object is not extensible
```

### 16.5.2 객체 밀봉

Object.seal 메서드는 객체를 밀봉한다. 밀봉된 객체는 읽기와 쓰기만 가능하다.

[예제 16-11]

``` javascript
const person = { name: 'Lee' };

// person 객체는 밀봉(seal)된 객체가 아니다.
console.log(Object.isSealed(person)); // false

// person 객체를 밀봉(seal)하여 프로퍼티 추가, 삭제, 재정의를  금지한다.
Object.seal(person);

// person 객체는 밀봉(seal)된 객체다.
console.log(Object.isSealed(person)); // true

// 밀봉(seal)된 객체는 configurable이 false다.
console.log(Object.getOwnPropertyDescriptors(person));
/*
{
    name: { value: "Lee", writable: true, enumerable: true, configurable: false }
}
*/

// 프로퍼티 추가가 금지된다.
person.age = 20; // 무시. strict mode에서는 에러
console.log(person); // { name: "Lee" }

// 프로퍼티 삭제가 금지된다.
delete person.name; // 무시. strict mode에서는 에러
console.log(person); // { name: "Lee" }

// 프로퍼티 값 갱신은 가능하다.
person.name = 'Kim';
console.log(person); // { name: "Kim" }

// 프로퍼티 어트리뷰트 재정의가 금지된다.
Object.defineProperty(person, 'name', { configurable: true });
// TypeError: Cannot redefine property: name
```

### 16.5.3 객체 동결

Object.freeze 메서드는 객체를 동결한다. 동결된 객체는 읽기만 가능하다.

[예제 16-12]

``` javascript
const person = { name: 'Lee' };

// person 객체는 동결(freeze)된 객체가 아니다.
console.log(Object.isFrozen(person)); // false

// person 객체를 동결(freeze)하여 프로퍼티 추가, 삭제, 재정의, 쓰기를  금지한다.
Object.freeze(person);

// person 객체는 동결(freeze))된 객체다.
console.log(Object.isFrozen(person)); // true

// 동결(freeze)된 객체는 writable과 configurable이 false다.
console.log(Object.getOwnPropertyDescriptors(person));
/*
{
    name: { value: "Lee", writable: false, enumerable: true, configurable: false }
}
*/

// 프로퍼티 추가가 금지된다.
person.age = 20; // 무시. strict mode에서는 에러
console.log(person); // { name: "Lee" }

// 프로퍼티 삭제가 금지된다.
delete person.name; // 무시. strict mode에서는 에러
console.log(person); // { name: "Lee" }

// 프로퍼티 값 갱신이 금지된다.
person.name = 'Kim'; // 무시. strict mode에서는 에러
console.log(person); // { name: "Lee" }

// 프로퍼티 어트리뷰트 재정의가 금지된다.
Object.defineProperty(person, 'name', { configurable: true });
// TypeError: Cannot redefine property: name
```

# 17장 생성자 함수에 의한 객체 생성

## 17.2 생성자 함수

### 17.2.5 constructor와 non-constructor의 구분

- constructor: 함수 선언문, 함수 표현식, 클래스(클래스도 함수다)
- non-constructor: 메서드(ES6 메소드 축약 표현), 화살표 함수

[예제 17-15]

``` javascript
// 일반 함수 정의: 함수 선언문, 함수 표현식
function foo() {}
const bar = function () {};
// 프로퍼티 x의 값으로 할당된 것은 일반 함수로 정의된 함수다. 이는 메서드로 인정하지 않는다.
const baz = {
    x: function () {}
};

// 일반 함수로 정의된 함수만이 constructor다.
new foo(); // -> foo {}
new bar(); // -> bar {}
new baz.x(); // -> x {}

// 화살표 함수 정의
const arrow = () => {};

new arrow(); // TypeError: arrow is not a constructor

// 메서드 정의: ES6의 메서드 축약 표현만 메서드로 인정한다.
const obj = {
    x() {}
};

new obj.x(); // TypeError: obj.x is not a constructor
```

### 17.2.7 new.target

함수 내부에서 new.target을 사용하여 new 연산자와 생성자 함수로서 호출했는지 확인

[예제 17-19]

``` javascript
// 생성자 함수
function Circle(radius) {
    // 이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined다.
    if (!new.target) {
        // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환한다.
        return new Circle(radius);
    }

    this.radius = radius;
    this.getDiameter = function () {
        return 2 * this.radius;
    };
}

// new 연산자 없이 생성자 함수를 호출하여도 new.target을 통해 생성자 함수로서 호출된다.
const circle = Circle(5);
console.log(circle.getDiameter());
```

# 18장 함수와 일급 객체

## 18.1 일급 객체

다음과 같은 조건을 만족하는 객체를 일급 객체라 한다.

1. 무명의 리터럴로 생성할 수있다. 즉, 런타임에 생성이 가능하다.
2. 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
3. 함수의 매개변수에 전달할 수 있다.
4. 함수의 반환값으로 사용할 수 있다.

## 18.2 함수 객체의 프로퍼티

### 18.2.1 arguments 프로퍼티

arguments 객체는 함수 호출 시 전달된 인수argument 들의 정보를 담고 있는 순회 가능한iterable 유사 배열 객체이며, 함수 내부에서 지역 변수처럼 사용된다.

[예제 18-04]

``` javascript
function multiply(x y) {
    console.log(arguments);
    return x * y;
}

console.log(multiply());            // NaN
console.log(multiply(1));           // NaN
console.log(multiply(1, 2));        // 2
console.log(multiply(1, 2, 3));     // 2
```

arguments 객체는 매개변수 개수를 확정할 수 없는 가변 인자 함수를 구현할 떄 유용하다.

[예제 18-06]

``` javascript
function sum() {
    let res = 0;

    // arguments 객체는 length 프로퍼티가 있는 유사 배열 객체이므로 for 문으로 순회할 수 있다.
    for (let i = 0; i < arguments.length; i++) {
        res += arguments[i];
    }

    return res;
}

console.log(sum());         // 0
console.log(sum(1, 2));     // 3
console.log(sum(1, 2, 3));  // 6
```

ES6의 Rest 파라미터 사용

[예제 18-08]

``` javascript
// ES6 Rest parameter
function sum(...args) {
    return args.reduce((pre, cur) => pre + cur, 0);
}

console.log(sum(1, 2));             // 3
console.log(sum(1, 2, 3, 4, 5));    // 15
```

### 18.2.3 length 프로퍼티

함수 객체의 length 프로퍼티는 함수를 정의할 때 선언한 매개변수의 개수를 가리킨다.

[예제 18-10]

``` javascript
function foo() {}
console.log(foo.length);    // 0

function bar(x) {
    return x;
}
console.log(bar.length);    // 1

function baz(x, y) {
    return x * y;
}
console.log(baz.length);    // 2
```

### 18.2.4 name 프로퍼티

함수 객체의 name 프로퍼티는 함수 이름을 나타낸다.

[예제 18-11]

``` javascript
// 기명 함수 표현식
var namedFunc = function foo() {};
console.log(namedFunc.name); // foo

// 익명 함수 표현식
var anonymousFunc = function() {};
// ES5: name 프로퍼티는 빈 문자열을 값으로 갖는다.
// ES6: name 프로퍼티는 함수 객체를 가리키는 변수 이름을 값으로 갖는다.
console.log(anonymousFunc.name); // anonymousFunc

// 함수 선언문(Function declaration)
function bar() {}
console.log(bar.name); // bar
```