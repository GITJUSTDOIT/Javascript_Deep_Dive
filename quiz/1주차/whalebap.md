# 1주차 Quiz

1. JS의 데이터타입 중 undefined와 null의 차이를 말하시오.
2. 다음 코드의 결과값을 말하시오.

    ```jsx
    var user = {name : 'Jisoo'}
    var admin = user
    var manager = {name : 'Jisoo'}

    admin.age = 26

    console.log(user)
    console.log(user===manager)
    console.log(user.name==manager.name)
    ```

---

1. **undefined : JS엔진이 변수를 초기화할 때 사용하는 값**. 변수 선언에 의해 확보된 메모리 공간에 할당이 이루어질 때까지 자바스크립트 엔진이 변수를 undefined로 초기화함. 
→ 변수 참조 시 undefined가 반환되면 초기화되지 않은 변수란 걸 알 수 있음. 
**null : 개발자가 변수에 값이 없다는 것을 의도적으로 명시하는 값.** 변수에 null을 할당하면 변수가 이전에 참조하던 값을 더 이상 참조하지 않는다는 의미. 
=할당된 값에 대한 참조를 명시적으로 제거
2. 

```jsx
1) console.log(user) // {name : 'Jisoo', age : 26}
2) console.log(user===manager) // false
3) console.log(user.name==manager.name) //true
```

1) 객체의 **참조에 의한 전달**에 때문에 객체 user에 프로퍼티 age가 생성된다. 원본 user와 사본 admin은 동일한 참조값을 가지며 동일한 객체를 가리킨다.  원본 또는 사본 중 어느 한 쪽의 객체를 변경하면 서로 영향을 주고 받는다. 

2)  === 연산자는 변수에 저장되어 있는 값을 타입 변환하지 않고 비교한다.  **객체를 할당한 변수를 비교하면 참조 값을 비교**한다. 객체 리터럴은 평가할 때마다 객체를 생성한다. 고로 객체 user와 manager는 다른 메모리에 저장된 별개의 객체로 참조값이 다르다. 

3)  **=== 연산자로 원시값을 할당한 변수를 비교하면 원시값을 비교**한다. 프로퍼티 name은 원시값 string을 평가한다.