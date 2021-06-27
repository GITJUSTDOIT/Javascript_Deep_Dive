## 문제 1.

1번과 2번의 출력값은?

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.getName = function () {
  return this.name;
};

const me = new Person("Lee");

console.log(me.getName()); //1번

Person.prototype.name = "Kim";

console.log(Person.prototype.getName()); //2번
```

## 문제2.

var 키워드로 선언한 변수는 코드 실행 단계에서 변수 선언문 이전에도 참조 할 수 있다. 그 이유를 설명하시오.

## 문제3.

정적 메서드와 프로토타입 메서드의 차이를 서술하시오.

## 문제4.

서브클래스의 constructor에서 반드시 super를 호출해야 하는 이유를 설명하시오.

---

## 정답 1.

1번 : getName 메서드를 호출한 객체는 me다. 따라서 getName 메서드 내부의 this는 me를 가리키며 this.name은 'Lee'다.

2번 : getName 메서드를 호출한 객체는 Person.prototype이다. Person.prototype도 객체이므로 직접 메서드를 호출할 수 있다. 따라서 getName 메서드 내부의 this는 Person.prototype을 가리키며 this.name은 'Kim'이다.

## 정답2.

전역 코드 평가 시점에 객체 환경 레코드에 바인딩 된 BindingObject를 통해 전역 객체의 프로퍼티와 메서드가 되기 때문이다. (전역 객체에 변수 식별자를 키로 등록한다.)

## 정답3.

- 정적 메서드와 프로토타입 메서드는 자신이 속해 있는 프로토타입 체인이 다르다.

- 정적 메서드는 클래스로 호출되고 프로토타입 메서드는 인스턴스로 호출한다.

- 정적 메서드는 인스턴스 프로퍼티를 참조할 수 없지만 프로토타입 메서드는 인스턴스 프로퍼티를 참조할 수 있다.

## 정답4.

서브클래스는 자신이 직접 인스턴스를 생성하지 않고 수퍼클래스에게 인스턴스 생성을 위임하기 때문이다.
