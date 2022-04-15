# Singleton
싱글톤 패턴이란?
싱글톤 패턴은 간단히 말해서 **객체의 인스턴스가 오직 1개만 생성되는 패턴**을 의미한다. 

최초 한번만 메모리를 할당(static)하고 그 메모리에 인스턴스를 만들어 사용하는 디자인 패턴이다. 
한번만 메모리를 할당하여 하나의 인스턴스를 만들고 생성한 객체를 반환한다. 여러 쓰레드가 동시에 해당 인스턴스를 공유하여 사용한다. 

요청이 많은 곳에서 사용하면 효율을 높일 수 있다. 하지만 **동시성(Concurrency)문제**를 고려해서 설계해야 한다.

## 싱글턴 패턴 구현 방법

1. Eager initialization, 이른 초기화(Thread-Safe)
2. Static block initialization
3. Lazy initialization
4. Thread Safe Singleton

### Eager initialization
``` java
public class EagerInitialization {
    private static final EagerInitialization instance = new EagerInitialization();
  
    private EagerInitialization(){}
  
    public static EagerInitialization getInstance() {
        retrun instance;
    }
}
```

### static block initialization
``` java
public class StaticBlockSingleton {
    private static StaticBlockSingleton instance;
    private StaticBlockSingleton(){}
    
    static {
        try {
            instance = new StaticBlockSingleton();
        }catch(Exception e){
            throw new RuntimeException("Exception occured in creating singleton instance");
        }
    }
    
    public static StaticBlockSingleton getInstance(){
        return instance;
    }
}
```

### Lazy Initailization
``` java
public class LazyInitialization(){
      private static LazyInitialization instance;
      
      priavate LazyInitailization(){}
      
      public static LazyInitailization getInstance(){
      
      if(instance==null){
          instance = new LazyInitailization();
      }
      return instance;
      }
}

```

### Thread Safe Singleton
``` java

public class ThreadSafeSingleton {
    private static ThreadSafeSingleton instance;
    
    private ThreadSafeSingleton(){}
    
    public static synchronized ThreadSafeSingleton getInstance() {
        if(instance == null){
            instance = new ThreadSafeSingleton();
        } 
        return instance;
    }
}
```

## 싱글톤 패턴을 사용하는 이유
싱글톤 패턴은 인스턴스가 오직 1개라는 특징이 있다. 1개의 인스턴스를 가지면 무엇이 좋을까?

- **메모리 절약**

최초 한번의 new 연산자를 통해 고정된 메모리 영역을 사용하기 때문에 추후 객체에 접근할 때 새로운 객체를 생성하지 않기 때문에 메모리 낭비를 방지할 수 있다.

- **시간 절약**

이미 생성된 인스턴스를 활용하니 객체 로딩 시간이 줄어들어 속도가 빨라져 성능이 좋아진다. 

- **데이터 공유 유용**

싱글톤 인스턴스가 전역으로 사용되는 인스턴스이기 때문에 다른 클래스의 인스턴스들이 접근하여 사용할 수 있다. 하지만 여러 클래스에서 싱글턴 인스턴의 데이터를 동시에 접근하게 되면 **동시성 문제가 발생**할 수 있다. 

(안드로이드 앱 같은 경우 서버와 통신할 때 retrofit 객체를 싱글톤으로 생성하여 접근하도록 설계한다.)

## 싱글톤 패턴의 문제점
싱글톤 패턴을 적용하면 위와 같은 장점도 있지만 단점도 존재한다. 

- **개방-폐쇄 원칙 위배**

싱글톤 인스턴스가 너무 많은 일을 하거나 많은 데이터를 공유할 경우에 다른 클래스의 인스턴스들 간에 결합도가 높아져 ‘개방-폐쇄 원칙’을 위배하게 된다. 이에 따라 수정이 어려워지고 유지보수의 비용이 높아질 수 있다. 

> 개방 폐쇄 원칙(OCP)란?
 확장에는 열려 있어야하고 변경에는 닫혀 있어야 한다. 즉, 기능을 변경하거나 확장할 수 있으면서 그 기능을 사용하는 코드는 수정하지 않는다. 

- **동기화 처리**

멀티쓰레드 환경에서 동기화 처리를 안하면 인스턴스가 2개가 생성될 수 있는 가능성이 생기게 된다. 


#### Reference
- [싱글톤(singleton 패턴이란?](https://tecoble.techcourse.co.kr/post/2020-11-07-singleton/)
- [싱글톤 패턴의 장단점](https://devmoony.tistory.com/43)
- [싱글톤 구현 방법](https://velog.io/@y_dragonrise/디자인-패턴-싱글톤-패턴Singleton-Pattern)
