1. 배열에서 push 메서드는 객체 자신을 변화시키는 부수 효과를 가져온다. 배열에서 push 메서드를 사용하지 않고 부수 효과 없이 요소를 추가할 수 있는 방법에 대해 설명해 보자

---

스프레드 문법을 사용하면 새로운 배열을 리턴할 수 있으므로 부수 효과가 없으며, 조금 더 직관적으로 사용할 수 있다.

``` javascript
const testArr = [1, 2, 3];

// push 메서드
testArr.push(4);    // testArr: [1, 2, 3, 4]

// 스프레드 문법
// testArr은 [1, 2, 3, 4]를 유지하고 5가 추가된 newTestArr의 사용이 가능해진다.
const newTestArr = [...testArr, 5]; // newTestArr: [1, 2, 3, 4, 5]
```