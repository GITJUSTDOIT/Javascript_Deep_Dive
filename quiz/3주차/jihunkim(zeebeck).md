## 3주차 Quiz
1. `makeCounter`를 사용해 두 개의 conuter `counter`와 `counter2`를 만들었다.

   두 counter는 독립적일까? 두 번째 카운터는 `0, 1`이나 `2, 3`중 어떤 숫자를 콘솔창에 띄워줄까? 

   ```javascript
   function makeCounter() {
     let count = 0;
   
     return function() {
       return count++;
     };
   }
   
   let counter = makeCounter();
   let counter2 = makeCounter();
   
   console.log( counter() ); // 0
   console.log( counter() ); // 1
   
   console.log( counter2() ); // ???
   console.log( counter2() ); // ???
   ```



2. 아래 코드의 실행 결과를 맞춰보자.

   ```javascript
   let phrase = "Hello";
   
   if (true) {
     let user = "John";
   
     function sayHi() {
       console.log(`${phrase}, ${user}`);
     }
   }
   
   sayHi();
   ```

   

---

1. 콘솔창엔 **0과 1** 이 출력된다.

   함수 `counter`와 `counter2`는 각각 다른 `makeCounter` 호출에 의해 만들어졌다.

   그리고, 두 함수는 독립적인 렉시컬 환경을 갖게 되므로 각 함수는 자신만의 `count`를 갖게 된다.

2. 에러가 발생.

   sayHi는 if문 안에서 정의했기 때문에, 오직 if문 안에서만 접근할 수 있다. if 문 밖엔 sayHi가 없다.