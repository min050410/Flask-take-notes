### CORS

### 목차
- cors란?
- cors를 해결하는 방법들
    - 프록시 서버 호스팅 or 구축
    - Access-Control-Allow-Origin 
    - 구글 플러그인 사용
    - 크롬에서 –disable-web-security 옵션을 추가
- Access-Control-Allow-Origin 헤더는 뭘까?
- cors를 사용하는 이유

### Cors란?
`교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)`는 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다.

웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행한다.

보안 상의 이유로, 브라우저는 교차 출처 HTTP 요청을 제한 한다. 그래서 `Cors`오류가 났던 것이다.

## Cors를 해결하는 방법들
### 프록시 서버 호스팅 or 구축
프록시 서버는 클라이언트가 프록시 서버 자신을 통해서 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해준다.  
쉽게 말해 브라우저와 서버 간의 통신을 도와주는 중계서버이다.  

```text
https://cors-anywhere.herokuapp.com
```
대표적으로 `heroku` `Proxy` 서버가 있다.  
이 서버를 사용하면 중간에 요청을 가로채서 `Access-Control-Allow-Origin : *` 를 설정해서 응답해준다.  

```js
axios({
    method: "GET"
    url: `https://cors-
anywhere.herokuapp.com/https://api.dropper.tech/covid19/status/korea?
locale=${city}`,
    headers: {
    'APIKey': COVID_APIKEY,
},
```

요청해야 하는 `URL`앞에 프록시 서버 `URL`을 붙여서 요청하게 되면,  
클라이언트에서 서버로 리소스를 요청할 때 발생하는 `Cors` 문제를 아주 간단하게 해결할 수 있다.

### Access-Control-Allow-Origin 

자신이 서버를 가지고 있다면 가장 쉽게 해결 하는 방법이다.
응답 헤더에 `Access-Control-Allow-Origin : *` 만 넣으면 해결 된다.  
만약 보안이 걱정된다면 특정 URL만
```text
Access-Control-Allow-Origin : https://devlog.kro.kr
```
이렇게 설정하는 것도 가능하다

또, 만약 `node.js` 서버라면 `pip install cors`와 설정을 통해 `Cors`해결이 가능하다.

### 구글 플러그인 사용
[여기](https://chrome.google.com/webstore/detail/allow-cors-access-control/lhobafahddgcelffkeicbaginigeejlf?hl=ko)
서 하면 된다던데 안해봐서 잘 모르겠다.

### 크롬에서 –disable-web-security 옵션을 추가
`-disable-web-security` 위와 같은 옵션을 `chrome` 실행시 붙여 사용하면 된다
`Chrome` 속성에 들어가 대상 url 뒤에 붙여 넣으면 쉽게 문제를 해결할 수 있다.
하지만 임시 방편의 방법이다.

### Access-Control-Allow-Origin 헤더는 뭘까?

`Access-Control-Allow-Origin` 헤더란 이 응답이 주어진 `origin`으로부터의 요청 코드와 공유될 수 있는지를 나타내는 헤더이다.

서버의 위치를 의미하는 https://google.com과 같은 URL들은 마치 하나의 문자열 같아 보여도, 사실은 여러 개의 구성 요소로 이루어져 있다
![image](https://user-images.githubusercontent.com/45661217/147995359-52b52ffc-2443-4071-8364-d782819f730b.png)
이때 `Origin`은 `Protocol`과 `Host`, 그리고 위 그림에는 나와있지 않지만 `:80`, `:443`과 같은 포트 번호까지 모두 합친 것을 의미한다.

### cors를 사용하는 이유
프론트엔드 개발자 들이 싫어하는 `cors`가 왜 세상에 나왔을까? 

악의를 가진 사용자가 소스 코드를 쓱 구경한 후 CSRF(Cross-Site Request Forgery)나 XSS(Cross-Site Scripting)와 같은 방법을 사용하여 애플리케이션에서 코드가 실행된 것처럼 꾸며서 사용자의 정보를 탈취하기가 너무나도 쉬워진다.
  
즉, 보안을 위해 적용한 것이다.




