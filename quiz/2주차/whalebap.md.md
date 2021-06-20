1. 다음 함수 주석 중 출력값이 틀린 것을 고르시오. 

```jsx
var a = 1;
var outer = function() {
	var inner = function() {
		console.log(a); //1
		var a = 3;
	};
	inner();
	console.log(a); //1
};
outer();
console.log(a) //1
```

2. 다음 함수는 1번의 키워드 var를 let으로 바꾼 것이다. 다음 함수의 출력값을 말하고 1과 다르다면 그 이유를 말하시오.

```jsx
let a = 1;
const outer = function() {
	const inner = function() {
		console.log(a);
		a = 3;
	};
	inner();
	console.log(a);
};
outer();
console.log(a)
```

---

1. inner 함수 안의 console.log(a)의 값은 undifined다. 
var a=1로 초기화 후 outer 함수가 실행되고 내부에 있는 inner 함수가 실행된다. 식별자 a에 접근할 때 현재 활성화 상태인 inner의 지역 스코프 안에서 a를 검색한다. a가 발견되지만 아직 할당된 값이 없어서 undfined로 출력된다. 이후 a에 3이 할당된다. 
outer 함수와 전역에서 호출한 a들은 함수를 호출한 지점의 렉시컬 스코프를 따르므로 inner 내 a의 값에 영향을 받지 않는다. 고로 전역에 선언된 a의 값을 따라 1이 출력도니다. 

2. 순서대로 콘솔에 1, 3, 3으로 찍힌다. 
ES6의 const, let은 함수레벨스코프인 var와 달리 블록레벨스코프를 가진다. 블록레벨스코프는 모든 코드블록(함수, if문, for문, whle문, try/catch문)을 지역 스코프로 인정한다. 전역 스코프-함수 레벨 스코프-블록 레벨 스코프 간 중첩이 일어난다. 
고로 inner 함수 내 console.log(a)는 전역 스코프에 선언된 a에 영향을, outer 함수 내 console.log(a)는 inner 함수에서 재할당된 a에 영향을, 전역 내 console.log(a)는 앞에서 3로 할당된 a에 영향을 받는다.