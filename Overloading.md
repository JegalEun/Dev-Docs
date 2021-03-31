# Overloading
자바에서 다형성을 지원하는 방법으로 메소드 `Overlading`과 `Overring`이 있다. 
> 다형성이란 같은 자료형에 여러 가지 객체를 대입하여 다양한 결과를 얻어내는 성질을 의미한다.

오늘은 그 중 오버로딩(Overloading)에 대해 알아보는 시간을 가질 것이다.

오버로딩은 **같은 이름의 메소드 여러개를 가지면서 매개변수의 유형과 개수가 다르도록 하는 기술**이다.

``` java
class OverloadingTest {
  void cat() {
    System.out.println("매개변수 없음");
  }
  
  void cat(int a, int b) {
    System.out.println("매개변수 :"+a+", "+b);
  }
  
  void cat(String c) {
    System.out.println("매개변수 : "+c);
  }
}

public class OverTest {

  public static void main(String[] args) {
  
    overloadingTest ot = new OverloadingTest();
    
    ot.cat();
    
    ot.cat(20,80);
    
    ot.cat("오버로딩 예제");
  }
}
```
실행을 해보면,

매개변수 없음

매개변수 :20, 80

매개변수 : 오버로딩 예제

를 확인할 수 있다.

예제를 보면 이름이 cat인 메서드가 총 3개가 있지만 각각 매개변수의 유형과 개수가 다른 것을 확인할 수 있다.

그리고 함수 호출 시 매개변수를 입력하면 호출 매개변수에 따라 매칭되어 함수를 실행시켜준다.

이것이 오버로딩이라고 한다.

## 오버로딩의 조건
- 메소드 이름 동일해야한다.
- 매개변수의 개수 또는 타입이 달라야 된다.
- 매개변수는 같고 리턴타입이 다른 경우는 오버로딩이 성립되지 않는다.

만약, 매개변수가 다르다면 오버로딩이 이루어지지 않는다.

위에 예제에서 

```java
void cat(String c) {
    System.out.println("매개변수 : "+c);
  }
``` 
매개변수의 타입을 `String`으로 하고,

```java
    ot.cat(10);
```
Main클래스에서 `String`이 아닌 `int`타입을 넣었다면 오버로딩이 되지 않는다.

## 오버로딩의 사용이유
오버로딩의 대표적인 예시로는 `System.out.println()`이 있다.

오버로딩이 만약 없다면?
출력할 값이 `char`,`boolean`,`String` 등등 타입에 따라 서로 다른 이름을 가져야하기 때문에 메소드를 작성하는 쪽에서는 이름을 짓기 어렵고, 메소드를 사용하는 쪽에서는 이름을 일일이 구분해서 기억해야하기 때문에 번거롭다.

하지만 오버로딩을 통해 여러 메소드들이 `println`이라는 하나의 이름으로 정의될 수 있다면, 기억하기도 쉽고 오류의 가능성을 많이 줄일 수 있다.

----
#### Reference
- [Overloading](https://private.tistory.com/25)
- [오버로딩과 오버라이딩](https://java119.tistory.com/32)
