## 4주차 Quiz
1. 객체 두 개를 이용해 쌍을 만들고 이를 수정하는 코드가 아래에 있다.

   얼럿창에 어떤 값이 나올지 예측해보자.

   ```javascript
   let animal = {
     jumps: null
   };
   let rabbit = {
     __proto__: animal,
     jumps: true
   };
   
   alert( rabbit.jumps ); // ? (1)
   
   delete rabbit.jumps;
   
   alert( rabbit.jumps ); // ? (2)
   
   delete animal.jumps;
   
   alert( rabbit.jumps ); // ? (3)
   ```

2. `animal`에서 상속받은 `rabbit`이 있다.

   `rabbit.eat()`을 호출했을 때, `animal`과 `rabbit` 중 어떤 객체가 `full` 프로퍼티를 받을까? 

```javascript
let animal = {
  eat() {
    this.full = true;
  }
};

let rabbit = {
  __proto__: animal
};

rabbit.eat();
```



---

1. `true` – `rabbit`에서 가져옴.

   `null` – `animal`에서 가져옴.

   `undefined` – 더 이상 프로퍼티를 찾을 수 없음.

2. **`rabbit`**

   점 앞에 있는 객체가 `this`가 되기 때문에, `rabbit.eat()`은 `rabbit`을 변경한다.

   프로퍼티를 찾는 것과 프로퍼티에 뭔가를 실행하는 것은 서로 다른 일이다.

   메서드 `rabbit.eat`은 프로토타입에서 처음으로 발견되지만, `this`엔 `rabbit`이 할당되어 실행된다.

