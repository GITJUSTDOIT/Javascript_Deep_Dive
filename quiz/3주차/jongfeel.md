1. 클로저에 대한 이해, 아래 코드에서 funcs array에서 실행했을 때의 출력 결과와 이런 클로저의 특징을 피해서 출력할 수 있는 방법에 대해 설명

``` javascript
var funcs = [];

for (var i = 0; i < 3; i++) {
    funcs[i] = function () { return i; };
}

for (var j = 0; j < funcs.length; j++) {
    console.log(funcs[j]());
}
```

---

let 변수로 선언해서 함수 레벨 스코프의 특징을 해결하여 for 문 작성. for문 내에서 새로운 렉시컬 환경을 만들어서 동작하므로 for문을 포함한 함수 레벨 스코프에서 let으로 정의할 때 클로저의 특징을 피할 수 있다.

``` javascript
var funcs = [];

for (let i = 0; i < 3; i++) {
    funcs[i] = function () { return i; };
}

for (let j = 0; j < funcs.length; j++) {
    console.log(funcs[j]());
}
```