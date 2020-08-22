# String, StringBuilder, StringBuffer의 차이점과 장단점
위에 세개는 문자열 클래스들이다. 모두 문자열을 저장하고 관리하는 클래스인데 무엇이 다를까?
면접 시 자주 나오는 질문 중에 하나여서 정리를 해보았다.

## String
'String'은 문자열을 대표하는 것으로 문자열을 조작하는 경우 유용하게 사용할 수 있다.

먼저 'String'과 다른 클래스(StringBuffer, StringBuilder)의 차이점은 String은 **immutable**(불변), 'StringBuffer'는 **mutable**(변함)에 있다.

'String' 객체는 한번 생성되면 할당된 메모리 공간이 변하지 않는다. 
'+연산자' 또는 'concat' 메소드를 통해 기존에 생성된 String 객체 문자열에 다른 문자열을 붙인다고 하자,
기존 문자열에 새로운 문자열을 붙이는 것이 아니라 새로운 String 객체를 만든 후, 새 String 객체에 연결된 문자열을 저장하고, 그 객체를 참조하도록 합니다. 
즉, 'String' 클래스 객체는 **Heap 메모리 영역**(가비지 컬렉션이 동작하는 영역)에 생성하고 한번 생성된 객체의 내부 내용을 변화시킬 수 없다. 

따라서 'String' 객체는 이러한 이유로 문자열 연산이 많은 경우, 그 성능이 좋지 않다.

하지만 'String' 객체와 같이 **Immutable**한 객체는 간단하게 사용가능하고 동기화에 대해 신경쓰지 않아도 되기때문에 내부 데이터를 자유롭게 공유 가능한다는 장점이 있다.

## StringBuffer와 StringBuilder
그러면 'StringBuffer'와 'StringBuilder' 클래스를 한번 보도록 하자

'StringBuffer'/'StringBuilder'는 'String'과 다르게 동작한다.
문자열 연산 등으로 기존 객체의 공간이 부족하게 되는 경우,

기존의 버퍼 크기를 늘리며 유연하게 동작한다. 'StringBuffer'와 'StringBuilder' 클래스가 제공하는 메서드는 서로 동일하다.

그렇다면 두 클래스의 차이점은 무엇일까?
바로 **동기화 여부**이다.

'StringBuffer'는 각 메서드별로 **Synchronized Keyword**가 존재하여, 멀티스레드 환경에서도 **동기화를 지원**한다.
반면, 'StringBuilder'는 동기화를 보장하지 않는다.

이러한 특성때문에 멀티스레드 환경이라면 값 동기화 보장을 위해 'StringBuffer'를 사용하고, 
단일스레드 환경이라면 'StringBuilder'를 사용하는 것이 좋다. 무조건적으로 단일스레드 환경에서는 'StringBuffer'를 사용해라!는 아니지만 동기화 관련 처리로 인해 'StringBilder'에 비해 성능이 좋지 않다.

----
#### Reference
- [String, StringBuffer, StringBuilder의 차이](https://12bme.tistory.com/42)
