# 1주차 퀴즈
### 문제   
```javascript 
// 1. 고객의 정보를 등록하는 화면에서 등록을 위해 유효성 검사를 한다고 가정 했을때 if문을 한 개 사용하여 코드를 간결하게 해주세요.
var phone = document.getElementById( "phone" ).innerText; // 변수 phone은 어떤값이 들어올지 모른다고 가정
if( phone === "" ) {
    alert( "오류가 발생 했습니다." );
    return false;
} 
if ( phone === null ) {
    alert( "오류가 발생 했습니다." );
    return false;
}
if ( phone === undefined ) {
    alert( "오류가 발생 했습니다." );
    return false;
}
// 서버로 전송
alert( "등록 완료!!!" );
```
***
### 정답
```javascript
if ( !phone ) {
    alert( "오류가 발생 했습니다." );
    return false;    
}
// 서버로 전송
alert( "등록 완료!!!" );
```
***
### 출제의도
```
회사에서 프로젝트 중 어떤 변수의 값이 정상적으로 들어왔을때 다음 로직으로 넘어가는데 빈값("")이 들어올지
null이 들어올지 모르는 상황에서 문제와 같이 썼다가 대리님의 조언으로 정답처럼 간결하게 쓰기 시작함    
```