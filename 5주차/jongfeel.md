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

# 35장 스프레드 문법

## 35.1 함수 호출문의 인수 목록에서 사용하는 경우

[예제 35-07]

``` javascript
const arr = [1, 2, 3];

// 스프레드 문법을 사용하여 배열 arr을 1, 2, 3으로 펼쳐서 Math.max에 전달한다.
// Math.max(...[1, 2, 3])은 Math.max(1, 2, 3)과 같다.
const max = Math.max(...arr);   // -> 3
```

## 35.2 배열 리터럴 내부에서 사용하는 경우

### 35.2.1 concat

[예제 35-10]

``` javascript
// ES6
const arr = [...[1, 2], ...[3, 4]];
console.log(arr);   // [1, 2, 3, 4]
```

### 35.2.2 splice

[예제 35-13]

``` javascript
// ES6
const arr1 = [1, 4];
const arr2 = [2, 3];

arr1.splice(1, 0, ...arr2);
console.log(arr1);  // [1, 2, 3, 4]
```

## 35.3 객체 리터럴 내부에서 사용하는 경우

스프레드 프로퍼티는 Object.assign 메서드를 대체할 수 있는 간편한 문법이다.

[예제 35-24]

``` javascript
// 객체 병합, 프로퍼티가 중복되는 경우 뒤에 위치한 프로퍼티가 우선권을 갖는다.
const merged = { ...{ x: 1, y: 2 }, ...{ y: 10, z: 3 } };
console.log(merged);    // { x: 1, y: 10, z: 3}

// 특정 프로퍼티 변경
const changed = { ... { x: 1, y: 2 }, y: 100 };
// changed = { ... { x: 1, y: 2 }, ...{ y: 100 } };
console.log(changed); // { x: 1, y: 100 }

// 프로퍼티 추가
const added = { ... { x: 1, y: 2 }, z: 0 };
// added = { ... { x: 1, y: 2 }, ... { z: 0 } };
console.log(added); // { x: 1, y: 2, z: 0 }
```

# 36장 디스트럭처링 할당

## 36.1 배열 디스트럭처링 할당

[예제 36-02]

``` javascript
const arr = [1, 2, 3];

// ES6 배열 디스트럭처링 할당
// 변수 one, two, three를 선언하고 배열 arr을 디스트럭처링 하여 할당한다.
// 이때 할당 기준은 배열의 인덱스다.
const [one, two, three] = arr;

console.log(one, two, three);   // 1, 2, 3
```

배열 디스트럭처링 할당을 위한 변수에 기본값을 설정할 수 있다.

[예제 36-07]

``` javascript
// 기본값
const [a, b, c = 3] = [1, 2];
console.log(a, b, c);   // 1, 2, 3

// 기본값보다 할당된 값이 우선한다.
const [e, f = 10, g = 3] = [1, 2];
console.log(e, f, g);   // 1, 2, 3
```

배열 디스트럭처링 할당을 위한 변수에 Rest 파라미터와 유사하게 Rest 요소 ...을 사용할 수 있다.\
Rest 요소는 Rest 파라미터와 마찬가지로 반드시 마지막에 위치해야 한다.

[예제 36-09]

``` javascript
// Rest 요소
const [x, ...y] = [1, 2, 3];
console.log(x, y);  // 1 [2, 3]
```

## 36.2 객체 디스트럭처링 할당

[예제 36-11]

``` javascript
const user = { firstName: 'Jongfeel', lastName: 'Kim' };

// ES6 객체 디스트럭처링 할당
// 변수 lastName, firstName을 선언하고 user 객체를 디스트럭처링하여 할당한다.
// 이때 프로퍼티 키를 기준으로 디스트럭처링 할당이 이루어진다. 순서는 의미가 없다.
const { lastName, firstName } = user;
console.log(firstName, lastName);   // Jongfeel Kim
```

객체의 프로퍼티 키와 다른 변수 이름으로 프로퍼티 값을 할당받으려면 다음과 같이 변수를 선언한다.

[예제 36-15]

``` javascript
const user = { firstName: 'Jongfeel', lastName: 'Kim' };

// 프로퍼티 키를 기준으로 디스트럭처링 할당이 이루어진다.
// 프로퍼티 키가 lastName인 프로퍼티 값을 ln에 할당하고,
// 프로퍼티 키가 firstName인 프로퍼티 값을 fn에 할당한다.
const { lastName: ln, firstName: fn } = usr;

console.log(fn, ln); // Jongfeel Kim
```

객체 디스트럭처링 할당은 객체에서 프로퍼티 키로 필요한 프로퍼티 값만 추출하여 변수에 할당하고 싶을 때 유용하다.

[예제 36-17]

``` javascript
const str = 'Hello';
// String 래퍼 객체로부터 length 프로퍼티만 추출한다.
const { length } = str;
console.log(length); // 5

const todo = { id: 1, content: 'HTML', completed: true };
// todo 객체로부터 id 프로퍼티만 추출한다.
const { id } = todo;
console.log(id); // 1
```

중첩 객체의 경우

[예제 36-21]

``` javascript
const user = {
    name: 'Lee',
    address: {
        zipCode: '03068',
        city: 'Seoul'
    }
};

// address 프로퍼티 키로 객체를 추출하고 이 객체의 city 프로퍼티 키로 값을 추출한다.
const { address: { city } } = user;
console.log(city);  // 'Seoul'
```

# 37장 Set과 Map

## 37.1 Set

### 37.1.1 Set 객체의 생성

중복을 허용하지 않는 Set 객체의 특성을 활용하여 배열에서 중복된 요소를 제거할 수 있다.

[예제 37-03]

``` javascript
// 배열의 중복 요소 제거
const uniq = array => array.filter((v, i, self) => self.indexOf(v) === i);
console.log(uniq([2, 1, 2, 3, 4, 3, 4]));   // [2, 1, 3, 4]

// Set 을 사용한 배열의 중복 요소 제거
const uniq = array => [...new Set(array)];
console.log(uniq([2, 1, 2, 3, 4, 3, 4]));   // [2, 1, 3, 4]
```

### 37.1.8 집합연산

- 교집합, Set.intersection()
- 합집합, Set.union()
- 차집합, Set.difference()
- 부분 집합과 상위 집합, Set.isSuperSet()

## 37.2 Map

### 37.2.1 객체의 생성

[예제 37-27]

``` javascript
const map1 = new Map([['key1', 'value1'], ['key2', 'value2']]);
console.log(map1);  // Map(2) { "key1" => "value1", "key2" => "value2" }

const map2 = new Map([1, 2]);   // TypeError: Iterator value 1 is not an entry object
```