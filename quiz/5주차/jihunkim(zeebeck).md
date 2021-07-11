## 5주차 Quiz
1. 아래 DOM 노드에 접근할 방법을 최소 한 가지 이상 적어보시오.

   - `<div>` DOM 노드
   - `<ul>` DOM 노드
   - 두 번째 `<li>` (Jane)

   ```javascript
   <html>
   <body>
     <div>사용자:</div>
     <ul>
       <li>John</li>
       <li>Jane</li>
     </ul>
   </body>
   </html>
   ```

2. 임의의 DOM 요소 노드 `elem`이 있다고 가정해보자.

   - `elem.lastChild.nextSibling`은 항상 `null`일까?
   - `elem.children[0].previousSibling`은 항상 `null`일까?

---

1. 방법은 다양하다.

   <div> DOM 노드:

   ```javascript
   document.body.firstElementChild
   // 또는
   document.body.children[0]
   // 또는 (첫 번째 노드는 공백이므로 두 번째 노드를 가져옴)
   document.body.childNodes[1]
   ```

   `<ul>` DOM 노드:

   ```javascript
   document.body.lastElementChild
   // 또는
   document.body.children[1]
   ```

   두 번째 `<li>` (Jane):

   ```javascript
   // <ul>을 가져오고, <ul>의 마지막 자식 요소를 가져옴
   document.body.lastElementChild.lastElementChild
   ```

2. 응 맞다. `elem.lastChild`는 항상 마지막 노드이기 때문에 `nextSibling`이 없다.

   아니다. `elem.children[0]`은 *요소 노드 중* 첫 번째 자식 노드를 나타내기 때문인데 이 앞에 요소 노드가 아닌 다른 노드가 올 수도 있다. `previousSibling`은 텍스트 노드가 될 수도 있다.

주의 사항: 두 경우 모두 자식 노드가 없는 경우 에러가 발생한다.

자식 노드가 없으면 `elem.lastChild`은 `null`이 되기 때문에 `elem.lastChild.nextSibling`에 접근할 수 없다. 그리고 컬렉션 `elem.children`은 빈 배열 `[]`같이 빈 상태가 된다.
