# TIL
> TypeScript today I learned
### TypeScript 코드 보기
- <a href="https://github.com/min050410/TechBlog">기술 블로그</a>

> #1

- `JavaScript` backtick syntax => \`  
`JavaScript` 억음 부호 문법

python 의 `f string` 처럼 사용 가능  
사용 예시
```ts
//기존의 js 문법
const welcome = 'You have logged in as ' + first + ' ' + last + '.'

const db = 'http://' + host + ':' + port + '/' + database;
```
```ts
//backtick 문법
const welcome = `You have logged in as ${first} ${last}`;

const db = `http://${host}:${port}/${database}`;
```
> #2

- 타입 표기  
타입스크립트 코드에서 어떤 변수 또는 값의 __타입__을 표기하기 위해 타입 표기를 사용한다.  
타입 표기는 `식별자` 또는 `값` 뒤에 콜론(:)을 붙여 `value: type` 의 형태로 표기한다.
```ts
// example
const areYouCool: boolean = true;
const answer: number = 42;
```

> #3

왜 `typeScript` 를 쓰는가?
  
- 보다 빠른 버그 발견
  - `type`이 정적이기 때문에 빠른 버그 발견이 가능
  - `js` 보다 `15%` 더 정확한 오류 검토 가능
- 에디터의 자동 완성 기능 증가
  - `type`을 안다면 더 정확한 자동 완성 기능 사용 가능
- `TypeScript`는 대부분 경우 안전한 코드를 작성할 수 있다
     
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
    if (arg.x !== null) {
        window.alert('arg.x is string!');
        // 이렇게 조건 검사를 다시 하도록 강제해야 한다
        if (arg.x !== null) {
          console.log(arg.x.substr(0, 3));
        }
    }
   }
  ```
  이런 점이 `TypeScript`가 안정성을 추구하는 방향이다
