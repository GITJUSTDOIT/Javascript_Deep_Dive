1. 객체를 생성하는 방법 중 {} 리터럴로 생성하는 방법과 new 로 생성하는 방법에 대해 설명해 보자.
2. 객체 프로퍼티에 값을 할당하는 방법이 두 가지가 있는데 각각 어떻게 할당할 수 있는지 설명해 보자.

---

1. 객체를 생성하는 방법

### {} 리터럴로 생성

``` javascript
let cat = {
    name: "choco",
    age: 1
};

console.log(cat); // { name: "choco", age: 1 }
```

### new로 생성

``` javascript
function Cat(name, age) {
    this.name = name;
    this.age = age;
}

let cat2 = new Cat("yam", 2);
console.log(cat2); // { name: "yam", age: 2 }
```

2. 객체 프로퍼티 할당

### 직접 프로퍼티에 접근

``` javascript
let cat = {
    name: "choco",
    age: 1
};

cat.age = 3;

console.log(cat); // { name: "choco", age: 3 }
```

### 대괄호 사용해서 접근

``` javascript
let cat = {
    name: "choco",
    age: 1
};

cat["age"] = 3;

console.log(cat); // { name: "choco", age: 3 }
```