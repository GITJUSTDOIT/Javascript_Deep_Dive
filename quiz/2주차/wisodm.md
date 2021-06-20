### 1. o2.x의 값은?
```
const obj = { x: 10, getSomething: () => console.log("test")}
const o1 = obj
const o2 = obj

o1.x=20
o2.x 
```

### 2. hasOwnProperty 메서드란?

-- ------------

1. 20 
2. hasOwnProperty 메서드는 이름에서 알 수 있듯이 인수로 전달받은 프로퍼티 키가 객체 고유의 프로퍼티 키인 경우에만 true를 반환하고 상속받은 프로토타입의 프로퍼티 키인 경우 false를 반환한다. 
