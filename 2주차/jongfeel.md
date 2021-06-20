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
- 변경이 발생하지 않고 읽기 전용으로 사용하는(재할당이 필요 없는 상수) 원시 값과 객체에는 const 키워드를 사용한다. const 키워든느 재할당을 금지하므로 var, let 키워드보다 안전하다.

