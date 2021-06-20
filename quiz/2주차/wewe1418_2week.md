# 2주차 퀴즈
---
## console.log()의 출력값을 확인하세요.
```javascript
var name = "linda";
console.log(this.name); // 1번

this.code = "21YK_00002";
console.log(code); // 2번

var num2 = 10;

var obj = {
    code : "21YK_00001",
    price : 5000000,
    name : "yuta",
    fun : function() {
        console.log(this.name); // 3번 
        console.log(this.code); // 4번
    },
    fun2 : function() {
        console.log(this.num2); // 5번
    }
}

obj.fun(); // 3번, 4번
obj.fun2(); // 5번

var num2Show = obj.fun2;
console.log(num2Show()); // 6번
```
## 정답
1번 -> linda   
2번 -> 21YK_00002   
3번 -> yuta   
4번 -> 21YK_00001  
5번 -> undefined   
6번 -> 10   
