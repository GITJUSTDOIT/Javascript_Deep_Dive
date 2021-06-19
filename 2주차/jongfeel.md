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