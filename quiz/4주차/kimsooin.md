# 4주차

## 문제1.

다음 코드에서 forEach메서드의 콜백 함수 내부의 this와 multyply 메서드 내부의 this를 일치시키기 위한 방법은?

```javascript
class Numbers {
  numberArray = [];
  multyply(arr) {
    arr.forEach(function (item) {
      this.numberArray.push(item * item);
    });
  }
}

const numbers = new Numbers();
numbers.multyply([1, 2, 3]);
```

## 문제2.

forEach, map, filter 메서드가 반환하는 값을 각각 서술하시오.

---

## 정답1.

forEach 메서드의두 번째 인수로 forEach 메서드의 콜백함수 내부에서 this로 사용할 객체를 전달하면 된다.

```javascript
class Numbers {
  numberArray = [];
  multyply(arr) {
    arr.forEach(function (item) {
      this.numberArray.push(item * item);
    }, this);
  }
}

const numbers = new Numbers();
numbers.multyply([1, 2, 3]);
```

## 정답2.

forEach 메서드는 undefined를 반환하고, map 메서드는 콜백함수의 반환값들로 구성된 새로운 배열을 반환하고 filter 메서드는 콜백 함수의 반환값이 true인 요소만 추출한 새로운 배열을 반환한다.
