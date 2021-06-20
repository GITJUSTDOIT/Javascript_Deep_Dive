1. 옵셔널 체이닝 연산자(?,)와 null 병합 연산자(??)의 차이점은?

2. 1번과 2번의 반환값은?

   var person 1 = {  
    name:'Lee'  
   };  
   var person 2 ={  
    name:'Lee'  
   };  
   console.log(person1 === person2) //1번
   console.log(person1.name === person2 name) //2번

---

1.  옵셔널 체이닝 연산자는 좌항의 피연산자가 null 또는 undefined 인 경우 undefined를 반환하고 그렇지 않으면 우항의 프로퍼티 참조를 이어가는 반면  null 병합 연산자는
    좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고 그렇지 않으면 좌항의 피연산자를 반환한다.

2.  *1번 : person1 변수와 person2 변수가 가리키는 객체는 내용은 같지만 다른 메모리에 저장된 별개의 객체 이므로 False!  
    *2번 : 프로퍼티 값을 참조하는 person.name과 person2.name은 값으로 평가될 수 있는 표현식이다. 표현식 모두 원시 값 'Lee'로 평가된다. 따라서 True!
