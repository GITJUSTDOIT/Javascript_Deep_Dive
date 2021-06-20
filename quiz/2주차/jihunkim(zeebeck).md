## 2주차 Quiz

1. min(a, b) 함수 만들기

   `a`와 `b` 중 작은 값을 반환해주는 함수, `min(a,b)`을 만들어보자.

   만든 함수는 아래와 같이 동작해야 한다.

   ```javascript
   min(2, 5) == 2
   min(3, -1) == -1
   min(1, 1) == 1
   ```

2. pow(x, n) 함수 만들기

   `x`의 `n`제곱을 반환해주는 함수, `pow(x,n)`를 만들어보자.  `x`의 `n` 제곱은 `x`를 `n`번 곱해서 만들 수 있다.

   ```javascript
   pow(3, 2) = 3 * 3 = 9
   pow(3, 3) = 3 * 3 * 3 = 27
   pow(1, 100) = 1 * 1 * ...* 1 = 1
   ```

   프롬프트 대화상자를 띄워 사용자로부터 `x`와 `n`을 입력받고 `pow(x,n)`의 반환 값을 보여주는 코드를 작성해 보자.

   주의사항: `n`은 `1` 이상의 자연수이어야 합니다. 이외의 경우엔 자연수를 입력하라는 얼럿 창을 띄워주어야 한다.











---

1. `if`문을 사용한 해답:

   ```javascript
   function min(a, b) {
     if (a < b) {
       return a;
     } else {
       return b;
     }
   }
   ```

   물음표 연산자 `'?'`를 사용한 해답:

   ```javascript
   function min(a, b) {
     return a < b ? a : b;
   }
   ```

   참고. `a == b`인 경우엔 `a`나 `b` 중 어떤 것을 반환해도 상관없다.

   

2. ```javascript
   function pow(x, n) {
     let result = x;
   
     for (let i = 1; i < n; i++) {
       result *= x;
     }
   
     return result;
   }
   
   let x = prompt("x?", '');
   let n = prompt("n?", '');
   
   if (n < 1) {
     alert(`${n}은 양의 정수이어야 합니다.`);
   } else {
     alert( pow(x, n) );
   }
   ```

