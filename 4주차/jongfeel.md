# 26장 ES6 함수의 추가 기능

## 26.2 메서드

ES6 메서드는 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 갖는다.

[예제 26-09]

``` javascript
const base = {
    name: 'Lee',
    sayHi() {
        return `Hi! ${this.name}`;
    }
};

const derived = {
    __proto__: base,
    // sayHi는 ES6 메서드다. ES6 메서드는 [[HomeObject]]를 갖는다.
    // sayHi의 [[HomeObject]]는 derived.prototype을 가리키고
    // super는 sayHi의 [[HomeObject]]의 프로토타입인 base.prototype을 가리킨다
    sayHi() {
        return `${super.sayHi()}. how are you doing?`;
    }
};

console.log(derived.sayHi());   // Hi! Lee. how are you doing?
```

## 26.3 화살표 함수

### 26.3.1 화살표 함수 정의

객체 리터럴을 반환하는 경우 객체 리터럴을 소괄호 ()로 감싸 주어야 한다.

[예제 26-18]

``` javascript
const create = (id, content) => ({ id, content });
create(1, 'JavaScript'); // -> { id: 1, content: "JavaScript" }

// 위 표현은 다음과 동일하다.
const create = (id, create) => { return { id, content }; };
```

### 26.3.3 this

화살표 함수 내부에서 this를 참조하면 일반적인 식별자처럼 스코프 체인을 통해 상위 스코프에서 this를 탐색한다.

[예제 26-33]

``` javascript
// 화살표 함수는 상위 스코프의 this를 참조한다.
() => this.x;

// 익명 함수에 상위 스코프의 this를 주입한다. 위 화살표 함수와 동일하게 동작한다.
(function () { return this.x; }).bind(this);
```

클래스 필드 정의 제안을 사용하여 클래스 필드에 화살표 함수를 할당, 이 경우에는 인스턴스 프로퍼티

[예제 26-44]

``` javascript
// Bad
class Person {
    // 클래스 필드 정의 제안
    name = 'Lee';
    sayHi = () => console.log(`Hi ${this.name}`);
}

const person = new Person();
person.sayHi(); // Hi Lee
```

sayHi 클래스 필드는 인스턴스 프로퍼티이므로 다음과 같은 의미다.

[예제 26-45]

``` javascript
class Person {
    constructor() {
        this.name = 'Lee';
        // 클래스가 생성한 인스턴스(this)의 sayHi 프로퍼티에 화살표 함수를 할당한다.
        // 따라서 sayHi 프로퍼티는 인스턴스 프로퍼티다.
        this.sayHi = () => console.log(`Hi ${this.name}`);
    }
}
```

하지만 클래스 필드에 할당한 화살표 함수는 프로토타입 메서드가 아니라 인스턴스 메서드가 된다. 따라서 메서드를 정의할 때는 ES6 메서드 축약 표현으로 정의한 ES6 메서드를 사용하는 것이 좋다.

[예제 26-46]

``` javascript
// Good
class Person {
    // 클래스 필드 정의
    name = 'Lee';
    sayHi() { console.log(`Hi ${this.name}`); }
}

const person = new Person();
person.sayHi(); // Hi Lee
```