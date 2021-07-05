# 33장 7번째 데이터 타입 Symbol

## 33.2 심벌 값의 생성

### 33.2.1 Symbol 함수

다른 값과 절대 중복되지 않는 유일무이한 값이다.

[예제 33-01]

``` javascript
// Symbol 함수를 호출하여 유일무이한 심벌 값을 생성한다.
const mySymbol = Symbol();
console.log(typeof mySymbol);   // symbol

// 심벌 값은 외부로 노출되지 않아 확인할 수 없다.
console.log(mySymbol);  // Symbol()
```

심벌 값에 대한 설명이 같더라도 생성된 심벌 값은 유일무이한 값이다.

[예제 33-03]

``` javascript
// 심벌 값에 대한 설명이 같더라도 유일무이한 심벌 값을 생성한다.
const mySymbol1 = Symbol('mySymbol');
const mySymbol2 = Symbol('mySymbol');

console.log(mySymbol1 === mysymbol2);   // false
```

### 33.2.2 Symbol.for / Symbol.keyFor 메서드

Symbol.for 메서드는 인수로 전달받은 문자열을 키로 사용하여 키와 심벌 값의 쌍들이 저장되어 있는 전역 심벌 레지스트리global symbol registry에서 해당 키와 일치하는 심벌 값을 검색한다.

- 검색에 성공하면 새로운 심벌 값을 생성하지 않고 검색된 심벌 값을 반환한다.
- 검색에 실패하면 새로운 심벌 값을 생성하여 Symbol.for 메서드의 인수로 전달된 키로 전역 심벌 레지스트리에 저장한 후, 생성된 심벌 값을 반환한다.

[예제 33-07]

``` javascript
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 없으면 새로운 심벌 값을 생성
const s1 = Symbol.for('mySymbol');
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 있으면 해당 심벌 값을 반환
const s2 = Symbol.for('mySymbol');

console.log(s1 === s2); // true
```

## 33.3 심벌과 상수

자바스크립트에서 enum을 흉내 내어 사용하려면 다음과 같이 객체의 변경을 방지하기 위해 객체를 동결하는 Object.freeze 메서드와 심벌 값을 사용한다.

[예제 33-11]

``` javascript
// JavaScript enum
// Direction 객체는 불변 객체이며 프로퍼티 값을 유일무이한 값이다.
const Direction = Object.freeze({
    UP: Symbol('up'),
    DOWN: Symbol('down'),
    LEFT: Symbol('left'),
    RIGHT: Symbol('right')
});

const myDirection = Direction.UP;

if (myDirection === Direction.UP) {
    console.log('You are going UP.');
}
```

# 34장 이터러블

## 34.1 이터레이션 프로토콜

- 이터러블 프로토콜iterable protocol
  - ...이터러블은 for ... of 문으로 순회할 수 있으며 스프레드 문법과 배열 디스트럭처링 할당의 대상으로 사용할 수 있다.
- 이터레이터 프로토콜iterator protocol
  - 이터러블의 Symbol.iterator 메서드를 호출하면 이터레이터 프로토콜을 준수한 이터레이터를 반환한다. 이터레이터는 next 메서드를 소유하며 next 메서드를 호출하면 이터러블을 순회하며 value와 done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환한다. 이러한 규약을 이터레이터 프로토콜이라 하며, 이터레이터 프로토콜을 준수한 객체를 이터레이터라 한다. 이터레이터는 이터러블 요소를 탐색하지 위한 포인터 역할을 한다.

### 34.1.1 이터러블

배열은 Array.prototype의 Symbol.iterator 메서드를 상속받는 이터러블이다.

[예제 34-02]

``` javascript
const array = [1, 2, 3];

// 배열은 Array.prototype의 Symbol.iterator 메서드를 상속받는 이터러블이다.
console.log(Symbol.iterator in array); // true

// 이터러블인 배열은 for...of 문으로 순회 가능하다.
for (const item of array) {
    console.log(item);
}

// 이터러블인 배열은 스프레드 문법의 대상으로 사용할 수 있다.
console.log([...array]);    // [1, 2, 3]

// 이터러블인 배열은 배열 디스트럭처링 할당의 대상으로 사용할 수 있다.
const [a, ...rest] = array;
console.log(a, rest); // 1, [2, 3]
```

## 34.3 for...of 문

[예제 34-07]

``` javascript
for (const item of [1, 2, 3]) {
    // item 변수에 순차적으로 1, 2, 3이 할당된다.
    console.log(item); // 1, 2, 3
}
```

위 예제의 for...of 문의 내부 동작을 for문으로 표현하면 다음과 같다.

[예제 34-08]

``` javascript
// 이터러블
const iterable = [1, 2, 3];

// 이터러블의 Symbol.iterator 메서드를 호출하여 이터레이터를 생성한다.
const iterator = iterable[Symbol.iterator]();

for (;;) {
    // 이터레이터의 next 메서드를 호출하여 이터러블을 순회한다.
    // 이때 next 메서드는 이터레이터 리절트 객체를 반환한다.
    const rest = iterator.next();

    // next 메서드가 반환한 이터레이터 리절트 객체의 done 프로퍼티 값이 true이면 이터러블의 순회를 중단한다.
    if (res.done) break;

    // 이터레이터 리절트 객체의 value 프로퍼티 값을 item 변수에 할당한다.
    const item = res.value;
    console.log(item);  // 1 2 3
}
```

### 34.6.3 이터러블이면서 이터레이터인 객체를 생성하는 함수

[예제 34-17]

``` javascript
// 이터러블이며서 이터레이터인 객체를 반환하는 함수
const fibonacciFunc = function (max) {
    let [pre, cur] = [0, 1];

    // Symbol.iterator 메서드와 next 메서드를 소유한 ㅣ터러블이면서 이터레이터인 객체를 반환
    return {
        [Symbol.iterator]() { return this; },
        // next 메서드는 이터레이터 리절트 객체를 반환
        next() {
            [pre, cur] = [cur, pre + cur];
            return { value: cur, done: cur >= max};
        }
    }
};

// iter는 이터러블이면서 이터레이터다.
let iter = finobacciFunc(10);

// iter는 이터러블이므로 for...of 문으로 순회할 수 있다.
for (const num of iter) {
    console.log(num); // 1 2 3 5 8
}

// iter는 이터러블이면서 이터레이터다.
iter = fiboncacciFunc(10);

// iter는 이터레이터이므로 이터레이션 리절트 객체를 반환하는 next 메서드를 소유한다.
console.log(iter.next());   // { value: 1, done: false }
console.log(iter.next());   // { value: 2, done: false }
console.log(iter.next());   // { value: 3, done: false }
console.log(iter.next());   // { value: 5, done: false }
console.log(iter.next());   // { value: 8, done: false }
console.log(iter.next());   // { value: 13, done: true }
```