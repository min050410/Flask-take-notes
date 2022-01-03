# TIL
> react-native today I learned 
### react-native 코드 보기
- <a href="https://github.com/min050410/RN_practice/tree/master">Simple Todo App</a>
- <a href="https://github.com/min050410/RN_practice/tree/navigation">Navigation Practice</a>
- <a href="https://github.com/min050410/NOTIFAM">NOTIFAM</a>
- <a href="https://github.com/min050410/App">AiforHuman</a>
> #1
- `components` 안에 기본적으로 나뉘는 js 파일들을 집어넣는다.  
* `components`    
  * `TodoInsert.js ` 
  * `TodoList.js` 
  * `TodoListItem.js`

(like this)  
  
> #2
- 훅 문법은 const App = () => {  
안에 넣는다   
```js
const [todos, setTodos] = useState([]);  
```
> #3 
- `node_modules`가 동작하지 않을때  
```terminal
$ npm install <module-name> --save  
```
출처: `https://xtring-dev.tistory.com/11`

> #4

`component` 분리 방법과 하는 법  
원래 #1 앞에 적었어야 했는데 후에 적음  
컴포넌트 파일 내에 앱 작성 + `export default`   
그 후 그 파일을 `import`, 파이썬 모듈 불러오는것과 비슷
```js
import TodoInsert from './components/TodoInsert';
```

> #5

`react native`로 쉽게 `API xml` 파싱하는법  
먼저,   
```terminal
npm install xml2js
```
`xml2js`를 다운한다.  
필자의 경우는 `string` 을 `xml`로 옮길 것이므로  
```js
import { parseString } from 'xml2js';
```
`parseString` 만 임포트 한다 
```js
parseString(text, function (err, result) {
                // console.log(result['lists']['list'][0]['PUM_NM_A']);
                setData(result['lists']['list'][0]['PUM_NM_A']);
                setPrice(result['lists']['list'][0]['AV_P_A']);
                setWeight(result['lists']['list'][0]['U_NAME']);
            })
```
그 후 이렇게 `parseString` 메서드를 이용해 `xml`로 파싱하고 값을 정상적으로 참조할 수 있다  

`xml2js`를 객체로 쓰고싶은 사람은
```js
var xml2js = require('xml2js');
var parser = new xml2js.Parser();
var fs = require('fs');
 
var xml = fs.readFileSync(__dirname + '/user.xml', 'utf-8');
 
parser.parseString(xml, function(err, result) {
  console.log(result);
});
```
이런 식으로 가능하다
  
아 그리고 __꿀팁__    
`react native`에서의 `console.log`는 `metro`에서 나온다 참고

> #6

`react native` `hook Usestate` 는 비동기이다.
```js
//3으로 생각하기 쉽지만 비동기 이기 때문에 마지막 함수만 실행됨
setIsloding(isloding+1);
setIsloding(isloding+1);
setIsloding(isloding+1);
```
- 간단하게 `동기`로 만드는 법
```js
//app.js
//useEffect 사용예시
const App = () => {
/...
useEffect(() => {
    goPhoto();
  }, [uploadData]);
/...
setuploadData(nowdata);
/...
}
export default App;
```
이렇게 하면 `uploadData`가 올라왔을때 `goPhoto()` 라는 함수가 실행된다  
그리고 `useEffect`를 `import` 하는걸 잊지 말자
```js
import {useState, useEffect} from 'react';
```
> #7

- Navigating Between Screens

`android studio` 의 `indent`를 `react native` 모듈로 구현 가능하다.
```node.js
// install
npm install @react-navigation/native @react-navigation/native-stack
npm install react-native-screens react-native-safe-area-context
```  
```js
return(
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Home"
          component={MainPage}
          //header 부분 삭제
          options={{ headerShown: false }}
        />
        <Stack.Screen 
          name="CapturePhoto" 
          component={CapturePhoto} 
          options={{ headerShown: false }}
        />
        <Stack.Screen 
          name="UploadPhoto" 
          component={UploadPhoto} 
          options={{ headerShown: false }}
        />
      </Stack.Navigator>
    </NavigationContainer>
```
app.js 에서 이렇게 선언하고 `component`에서는
```js
const CapturePhoto = ({navigation}) => {
//이렇게 매개변수 부분에 `navigation`을 넣고
//후에 결과창으로 리다이렉트
   navigation.navigate('resultpage');
//함수 안에서 이렇게 다른 페이지로 이동하면 된다
```
다른 컴포넌트로 `props`를 주고 싶을때가 있다
그럴때는
```js
<Button
      title="Go to Jane's profile"
      onPress={() =>
        navigation.navigate('Profile', { name: 'Jane' })
      }
// navigation.navigate 뒤에 { name: 'Jane' } 을 주고
const ProfileScreen = ({ navigation, route }) => {
  return <Text>This is {route.params.name}'s profile</Text>;
};
// ProfileScreen 에서 route.params.~~를 이용해 받을 수 있다.#
```
<a href="https://reactnative.dev/docs/navigation">참고한 웹사이트</a>

> #8
`react-native-camera` 적용 방법

정말 많은 오류가 떴고 `server error 500` 부터 시작해서 `package.json`오류,,  
많은 경험을 바탕으로 쉽고 빠르게 `react-native` 에 적용시키는 법을 알아보자!  
  
일단 다운을 받는다
```
npm i -s react-native-camera
react-native link react-native-camera
```
`package.json` 에 `dependencies`안 `react-native-camera`가 추가되었는지 확인한다
- `project`
  - `android`
    - `app`
      - `bulid.grandle` 안에서 `defaultConfig` 안에 이걸 집어넣는다
```java
missingDimensionStrategy 'react-native-camera', 'general'
```
그리고 안드로이드는 퍼미션을 줘야한다.
```java
// manifest 안에 추가
<!-- camera permission -->
<uses-permission android:name="android.permission.CAMERA" />
```
후에 `react-native run-android`
오류가 걸린다면 `package.lock`이나 `yarn.lock`을 제거하고 실행해본다


