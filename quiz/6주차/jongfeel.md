1. 아래와 같은 REST API를 fetch로 호출할 때 promise 문법을 써서 호출하면 결과를 얻을 수 있다.

``` javascript
const fetch = require('node-fetch');

fetch('https://jsonplaceholder.typicode.com/todos/1')
  .then(function(response) {
    return response.json();
  })
  .then(function(todo) {
    console.log(todo);
  });
```

여기서 async/await 문법을 적용해서 더 간결하게 코드를 작성해 보자.

---

fetch 함수는 promise 기반으로 작성할 수 있고, async/await을 사용할 수 있으므로 아래와 같이 작성 가능하다.

``` javascript
const fetch = require('node-fetch');

const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
const todo = await response.json();
console.log(todo);
```