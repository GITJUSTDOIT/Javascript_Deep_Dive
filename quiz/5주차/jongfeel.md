1. Symbol.for 함수의 기능을 설명하고 아래 코드의 결과가 true인지 false 인지 설명해 보자

``` javascript
let u1 = Symbol.for("unique1");
let u2 = Symbol.for("unique1");

console.log(u1 === u2);
```

---

Symbol.for 함수는

- 기존에 값이 있으면 symbol 값을 리턴한다.
- 기존에 값이 없다면 symbol 값을 레지스트리에 저장하고 그 값을 리턴한다.

따라서 첫번째 Symbol.for("unique1")의 경우는 레지스트리에 값이 없으므로 "unique1"이라는 키값으로 symbol 값을 가져온다.

그리고 두번째 Symbol.for("unique1")의 경우는 첫번째 라인에서 같은 값으로 심벌 값이 레지스트리에 저장이 되었으므로 그 심벌값을 가져오는 코드가 된다.

그래서 u1과 u2는 별개의 변수이지만 같은 심벌 값인 "unique1"을 가리키므로 결과는 true가 된다.