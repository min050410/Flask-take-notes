# react-native 카메라 적용 방법

시작하기 전,  
나는 `npm`을 사용하고 `react-native-cli`를 쓴다.

리액트 네이티브 카메라를 적용하는데 정말 많은 오류가 떴고 `server error 500` 부터 시작해서 `package.json`오류,, 등등   
많은 경험을 바탕으로 쉽고 빠르게 `react-native` 에 적용시키는 법을 알아보자!  
  
### react native camera 다운
```text
npm i -s react-native-camera
react-native link react-native-camera
```
`i`는 `install`의 줄임말이다  
`install`로 써도 무방하다

### react-native-camera 추가 확인
`package.json` 파일 안에 `dependencies`안 `react-native-camera`가 추가되었는지 확인한다

react-native-camera가 정상적으로 추가되었으면  
`project`-`android`-`app`-`bulid.grandle` 안에서 `defaultConfig` 안에 이 코드를 집어넣는다
```java
missingDimensionStrategy 'react-native-camera', 'general'
```
### android 권한 주기
그리고 안드로이드는 권한을 줘야한다.  
android menifest에 다음을 추가한다.
```java
// manifest 안에 추가
<!-- camera permission -->
<uses-permission android:name="android.permission.CAMERA" />
```
후에, `react-native run-android`로 빌드해본다
오류가 걸린다면 `package.lock`이나 `yarn.lock`을 제거하고 실행해본다