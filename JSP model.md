살짝(?) 늦은 감이 있지만 MVC에 대해 정확히 알아보고자 문서를 새로 작성하기로 하였다.

저번 시간에  MVC1, MVC2 model의 차이점을 알아보았는데 사실 MVC1, MVC2 model은 실제로 존재하지 않는다고 한다.

대개 사람들은 MVC2가 우리가 말하는 MVC model이라고 불리우는데, 이 둘은 완전히 다른 개념이고 MVC2는 남용되는 단어이다.

웹프로그래밍과 MVC에 대해 차근차근 알아보자.

# 웹 어플리케이션의 디자인 모델
웹 애플리케이션이란, 웹 브라우저와 사용자와 대화하는 대화식으로서 인터넷을 이용하는 일종의 컴퓨터 프로그램을 말한다.

웹 어플리케이션의 디자인에는 일반적으로 두 가지의 디자인 모델이 있다.

바로 `Model 1 JSP programming`, `Model 2 JSP programming`이다. 
이 것때문에 MVC1, MVC2라고 불리게 된 원인이다.

## Model 1 JSP programming
처음에 웹 개발은 `Sevlet`을 이용하여 그 안에 JAVA기술을 기입하고 개발였다. 하지만 `Sevlet`을 이용한 웹 페이지는 오류가 발생하기 쉬었고,
웹 디자이너들은 쓰여진 JAVA 코드를 이해해야하고 코드를 유지하면서 프레젠테이션 로직을 변경하는 것이 어려웠다. 

이 문제를 해결하기 위해서 `JSP`개념이 등장하게 되었고 디자이너는 JAVA 지식을 가질 필요가 없어졌다. 또한, `JSP`를 활용해 웹 디자이너는 프레젠테이션 로직만 따로 기술해 코드를 유지하는 것이 쉬워졌다.

이것이 바로 `Model 1 JSP programming`이라고 불려왔고 `MVC1`이라고도 잘못 불린 개념이다.

<img width="399" alt="JSP Model 1" src="https://user-images.githubusercontent.com/43868540/99762801-a919bb00-2b3c-11eb-9abc-0dbcaab37dea.png">

> [출처 wikipedia](https://en.wikipedia.org/wiki/JSP_model_1_architecture)

하지만 `JSP`를 이용한 프로그래밍도 단점이 있다. 개발자들은 `JSP`를 이용해 데이터베이스에서 접근하였고 `Sevlet`역할도 하였다. 따라서 요청 처리, 데이터 유효성 검사, 비즈니스 로직 처리 및 응답 등 요청에 대한 모든 책임을 `JSP`에서 처리하였다. 이것은 프레젠테이션 로직과 비즈니스 로직를 분리하지 못하는 또 다른 문제점이었다.

## MVC
프레젠테이션 로직과 비즈니스 로직을 분리하기 위해 Trygve Reenskaug가 `MVC` 패턴을 발명하였다.
`MVC`는 Model-View-Controller로 이루어져 프로그램 로직을 나누고 개발하는 소프트웨어 설계 패턴이다.

따라서
- `Sevlet`이 `Controller`역할을 하여 데이터와 비즈니스 로직 사이의 상호동작을 관리한다.
- 기존에 `JSP`에 쓰였던 프레젠테이션 로직을 `View`에 기술하여 인터페이스 요소를 나타내고
- 데이터베이스에 접근하기 위해 `Bean`과 `POJO 클래스`를 작성해 `Model`역할을 한다.

이렇게 로직을 분리해 대규모 프로그램을 개발하고 유지보수하기에 수월해졌다.

1. 사용자 요청이 Contoller(SERVLET)로 이동.

2. 요청받은 Controller는 비즈니스 요구사항을 충족하기 위해 필요한 모델(Bean)을 가져온다.

3. 응답 프레임을 설정하고 응답을 뷰 구성요소(JSP)로 전달한다.

## Model 2 JSP programming
이렇게 로직을 분리하여 개발한 프로그래밍이 `Model 2 JSP programming`이라고 한다. 이것 또한 역시 `MVC2`라고 잘못 불린 개념이다. 
`Model 2`는 비즈니스 로직과 프레젠테이션 로직을 분리하므로 일반적으로 MVC ( 모델-뷰-컨트롤러 ) 패러다임을 활용한 모델이라고 할 수 있다.

`Model 2`는 `Sevlet`이 `Controller` 역할을 하여 클라이언트의 요청을 전달받는다.


# 마치며
MVC1, MVC2 개념이 애초에 없던 개념이고 MVC, JSP model1, JSP model2 만 존재하였다.

아직까지 많은 사람들이 MVC 패턴이 MVC2 모델이라고 알고 있고 나 또한 그랬었다. 이번 시간을 통해 정확히 개념을 바로잡는 시간이 되었기를 바란다.

----
**** Reference
- [JSP 모델 1 아키텍쳐](https://en.wikipedia.org/wiki/JSP_model_1_architecture)
- [JSP 모델 2 아키텍쳐](https://en.wikipedia.org/wiki/JSP_model_2_architecture#cite_note-5)
- [MVC 패턴](https://ko.wikipedia.org/wiki/%EB%AA%A8%EB%8D%B8-%EB%B7%B0-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC)
- [MVC1과 MVC2의 차이](https://technicalrecyclebin.wordpress.com/2012/11/14/difference-between-mvc1-and-mvc2/)
