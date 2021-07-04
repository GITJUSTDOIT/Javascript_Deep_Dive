# 1번문제 스택을 구현해라

26강에서 32강까지를 통해 배운 명령어를 활용해보자


정수를 저장하는 스택을 구현한 다음, 입력으로 주어지는 명령을 처리하는 프로그램을 작성하시오.

명령은 총 다섯 가지이다.

push X: 정수 X를 스택에 넣는 연산이다.
pop: 스택에서 가장 위에 있는 정수를 빼고, 그 수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다.
size: 스택에 들어있는 정수의 개수를 출력한다.
empty: 스택이 비어있으면 1, 아니면 0을 출력한다.
top: 스택의 가장 위에 있는 정수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다.

문제풀기 : https://www.acmicpc.net/problem/10828




---

#정답
```javascript
//const input = require("fs").readFileSync("/dev/stdin").toString().trim().split("\n");


const input = ['14',
    'push 1',
    'push 2',
    'top',
    'size',
    'empty',
    'pop',
    'pop',
    'pop',
    'size',
    'empty',
    'pop',
    'push 3',
    'empty',
    'top'];
const stack = [];
const print = [];

for(let i = 1; i <= input[0]; i++) {
  let array = input[i].split(' ');
  let cmd = array[0];
    if(cmd === 'push') {
        stack.push(array[1]);
    } else if(cmd === 'pop') {
        print.push(stack.pop() || -1);
    } else if(cmd === 'size') {
        print.push(stack.length);
    } else if(cmd === 'empty') {
        print.push(stack.length ? 0 : 1);
    } else {
        print.push(stack[stack.length-1] || -1);
    }

} 
console.log(print.join('\n')); // 출력
