
# 1번 문제

다음 코드를 실행 할 때 increase함수에서는 n값이 0에서 시작해서 올라가지만 decrease함수에서는 n값이 0에서 시작해서 내려가기만한다
코드를 일부 수정해서 n값이 함수를 통해 증감이 연동될 수 있게 만드시오 (단, 고차 함수를 써야하며 위 코드처럼 클로저를 반환한다)
```javascript
function makeCount(predicate) {
    let count = 0;

    //클로저를 반환
    return function () {
        count = predicate(count);
        return count;
    };

}

function increase(n) {
    return ++n;
}

function decrease(n) {
    return --n;
}

const increaser = makeCount(increase);
console.log(increaser());

const decreaser = makeCount(decrease);
console.log(decreaser());
```

---

# 해결방법
```javascript
const count = (function () {
    let count = 0;

    //클로저를 반환
    return function (predicate) {
        count = predicate(count);
        return count;
    };

}());

function increase(n) {
    return ++n;
}

function decrease(n) {
    return --n;
}

console.log(count(increase));
console.log(count(decrease));
```

문제에 있는 `makeCount`함수를 호출해 함수를 반환할 때 반환된 함수는 자신만의 독립된 렉시컬 환경을 가진다
`const increaser`에 할당이 될 때 `makeCount` 함수의 실행 컨텍스트는 소멸이된다 하지만 `makeCount` 함수 실행 컨텍스트의 렉시컬 환경은 `makeCount` 함수가 반환한 함수의 `[[Environment]]` 내부 슬롯에 의해 참조되고 있기 때문에 소멸되지 않는다.
`const decreaser`도 마찬가지로 동작한다 새로운 `makeCount` 함수의 실행 컨텍스트를 생성하기 때문에 값이 전달되지 않는다(독립적이다)
함수를 사용해서 값이 연동될 수 있도록 하려면 `makeCount`를 사용해서 함수를 두 번 호출하는 행동을 해서는 안된다
`렉시컬 환경`과 `실행 컨텍스트` 그리고 `클로저`라는 개념을 알자


~~그건 그렇고 딥다이브 책을 읽을수록 변수를 엄청 헷갈리게 해놔서 읽기가 참 불편한 것 같다~~
































~~채팅창 화력 다죽었다~~
