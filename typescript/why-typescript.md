# 타입스크립트를 많이 쓰는 이유
**react** **ts**
> TypeScript I learned   
~~사실 이게 아니라 today다~~  

### 목차
- 왜 `typescript`를 쓰는가
- `typescript`의 단점


<h3 id="why">왜 typeScript 를 쓰는가?</h3>

- 보다 빠른 버그 발견
  - `type`이 정적이기 때문에 빠른 버그 발견이 가능
  - `js` 보다 `15%` 더 정확한 오류 검토 가능
- 에디터의 자동 완성 기능 증가
  - `type`을 안다면 더 정확한 자동 완성 기능 사용 가능
- `TypeScript`는 대부분 경우 안전한 코드를 작성할 수 있다  
  - TypeScript는 `컴파일` 타임에 어느 부분이 깨지는지 빠짐없이 알려주기 때문에 리팩토링하기 정말 편해진다.
     
### 타입스크립트의 단점
 
```ts
  // 이 코드를 보자
  // a의 x 타입은 string 이거나 null 이라고 지정한다
  function getFirstThreeCharsUnsafe(arg: { x: string | null }) {
    if (arg.x !== null) {
        window.alert('arg.x is string!');
        console.log(arg.x.substr(0, 3)); //오류가 생긴다
    }
  }
  // a.x 를 string ok로 설정
  var a: { x: string | null } = { x: 'ok' };
    window.alert = function (str: string) {
    a.x = null;
  };
  //함수 호출
  getFirstThreeCharsUnsafe(a);
```
```ts
  // 해결하기 위해서는 다음과 같이 함수를 고쳐야 한다
  function getFirstThreeCharsSafe(arg: { x: string | null }) {
    // 조건 검사 한번을 하고
    if (arg.x !== null) {
        window.alert('arg.x is string!');
        // 이렇게 함수마다 조건 검사를 다시 하도록 강제해야 한다
        if (arg.x !== null) {
          console.log(arg.x.substr(0, 3));
        }
    }
   }
  // a.x 를 string ok로 설정
  var a: { x: string | null } = { x: 'ok' };
    window.alert = function (str: string) {
    a.x = null;
  };
  //함수 호출
  getFirstThreeCharsUnsafe(a);
```

`typescript`는 이런 경우 안전함을 다소 희생하는 선택지와 프로그래머를 짜증나게 하더라도 안전성을 택하는 선택지 중 후자의 비용이 더 크다고 판단한다.   
때문에 이런 문제를 알고 있음에도 불구하고 `getFirstThreeCharsUnsafe` 와 같은 사용법을 허용한다.
이렇듯 타입 안정성을 일부 희생하면서 사용성을 극대화시키는 과감한 선택 덕에 타입스크립트 사용자는 생산성의 희생 없이도 대부분의 경우 안전한 코드를 작성할 수 있다.