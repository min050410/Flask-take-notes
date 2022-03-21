# cpp 예외처리 매커니즘 - try, catch, throw

우리에게 익숙한 예외 처리는 if 문을 이용한 예외처리이다. 하지만 if 문을 보고 예외처리를 위한 코드인지 쉽게 구분하지 못해 가독성이 떨어지는 단점이 있다.

그 단점을 보완하기 위해 cpp에 예외 처리 매커니즘이 존재한다.

가독성, 유지성, 보수성을 높일 수 있고,
예외의 처리를 일반적인 프로그램의 흐름에서 독립시키는 것이 가능하다.
```cpp
try {
    // 예외 발생 예상지역
}
```
try 블록은 예외 발생에 대한 검사의 범위를 지정할 때 사용된다.

```cpp
catch(처리할 예외의 종류 명시)
{
    // 예외처리 코드의 삽입
}
```
catch 블록은 try블록에서 발생한 예외를 처리하는 코드가 담기는 영역이다.
```cpp
throw expn;
```
throw는 예외가 발생했음을 알리는 문장의 구성에 사용된다.

expn은 예외상황에 대한 모든 정보를 담은, 의미 있는 데이터 이어야 한다.

```cpp
try{
    if(예외가 발생한다면)
    {
        throw expn;
    }
}
catch(type expn)
{
    // 예외의 처리
}
```
"throw에 의해 던져진 "예외" 데이터는, '예외' 데이터를 감싸는 try 블록에 의해 감지가 되어 이어서 등장하는 catch 블록에 의해 처리된다."