1. 객체를 생성할 때 객체 안에 있는 함수를 객체를 생성할 때 마다 메모리를 할당해서 생성하지 않고 prototype을 이용해 공유하는 방식으로 생성하는 방법에 대해 설명해 보자.

---

1. prototype을 사용하지 않고 객체를 생성하는 방법은 매번 같은 인스턴스를 중복해서 생성하는 문제가 있음

``` javascript
function Pet(name) {
    this.name = name,
    this.Name = () => this.name;
}

let myPet = new Pet('choco');
let yourPet = new Pet('happy');

// 두 객체의 Name() 함수는 공유해서 사용하지 않고 각각의 메모리 공간을 차지함
console.log(myPet.Name());
console.log(yourPet.Name());
```

따라서 prototype을 통해 Name() 함수를 정의하고 상속 구조를 통해 함수가 공유되서 객체가 생성될 때 각 객체의 함수로 참조할 수 있게 정의

``` javascript
function Pet(name) {
    this.name = name
}

Pet.prototype.Name = function() { return this.name; }

let myPet = new Pet('choco');
let yourPet = new Pet('happy');

// 이제 Name() 함수는 공유해서 사용하므로 Pet 객체가 100개가 만들어져도 Name() 함수가 100개가 생성되지 않는다
console.log(myPet.Name());
console.log(yourPet.Name());
```