# 1번 출력되는 값은?
const secret1 = Symbol('mySymbol');
const secret2 = Symbol('mySymbol');

console.log(secret1 === secret2);

# 2번 spread랑 rest문법은 ...을 사용하는데 차이점은?

# 3번 Set과Map이 공통적으로 에러를 내보내는 명령어는

---
# 정답
1. false
2. spread는 [1, 2] -> 1, 2 rest는 (function foo(...a)) 1, 2 -> [1, 2]
3. Set과 Map은 delete를 두번 연속 쓸 수 없다
