# SOAP API
API를 사용하면서 여러 종류의 API가 있다는 사실을 알게 되었다. 가장 대표적인 두 가지 방식으로는 SOAP와 REST가 있다.
SOAP와 REST는 일반적으로 웹 서비스라고 불린다. 이러한 서비스는 서로 다른 컴퓨터에서 네트워크를 통해 데이터를 주고 받는 통신이라고 생각하면 된다. 

저번 시간에는 은지언니가 REST API에 대해 자세히 알아보았다.
이번 시간에는 SOAP에 대해서 자세히 알아보는 시간을 가지자.

## SOAP API와 REST API?
SOAP는 Simple Object Access Protocol의 약자이며 HTTP, HTTPS, SMTP 등을 통해 XML 기반의 메시지를 컴퓨터 네트워크 상에서 교환하는 프로토콜이다.

SOAP는 보안 수준이 엄격하다. SSL도 지원하고 WS-Security라는 자체 표준의 보안 기능도 가지고 있다. 따라서 은행용 모바일 앱, 신뢰할 수 있는 메시징 앱 등 보안수준이 높아야하거나 또는 ACID를 준수해야하는 경우라면 SOAP방식이 더욱 선호된다.

ACID를 준수하기 때문에 데이터의 변형을 줄여주고, 데이터베이스와의 상호작용에 대해서 사전에 정확하게 정하기 때문에 데이터의 무결성을 지켜준다. 따라서 금융 정보 등의 민감한 데이터를 주고 받을 때 많이 사용된다. 

복습하는 의미로 REST API도 간단하게 정리해보자.

REST는 REpresentation State Transfer의 약자로 네트워크를 통해서 컴퓨터들끼리 통신할 수 있게 해주는 아키텍쳐 이다. 주로 JSON형식을 사용한다. 

REST API는 인터넷 식별자(URI)와 HTTP 프로토콜을 기반으로 한다. 데이터 포맷은 브라우저 간 호환성이 좋은 JSON을 사용한다. 
클라이언트와 서버 사이에서 통신을 할 수 있게 하고, 아키텍처를 만들 수 있게 해준다. 즉, 클라이언트-서버 모델로 구축되었다는 것을 의미한다. 

REST는 웹에 최적화되어 있고, 데이터 포맷이 JSON이기 때문에 브라우저들 간에 호환성이 좋다. 또한, 구축과 확장이 간단해 성능과 확장성이 뛰어나다. 

### SOAP의 장점과 단점
장점
- SOAP는 플랫폼과 프로그래밍 언어에 독립적이다.
- SOAP는 웹 서비스를 제공하기 위한 표준(WSDL, UDDI, WS-Security)이 잘 정립되어 있다.
- SOAP는 에러 처리에 대한 내용이 기본으로 내장되어 있다.
- SOAP는 분산 환경에 적합하다.

단점
- SOAP는 복잡한 구조로 인한 오버헤드가 있으며, 이는 SOAP의 확장을 저해한다.
- REST에 비해 구조가 복잡하기 때문에 상대적으로 무겁고 속도도 느리다.
- 메시지 인코딩/디코딩 과정 등 개발 난이도가 높아 개발환경의 지원이 필요하다.

### SOAP 아키텍처
SOAP는 일반적으로 UDDI 레지스토리를 통해 웹서비스를 등록(Publish)하고, 탐색(find)하고, 바인딩(Bind)하여 사용한다. 

![SOAP 동작원리](https://user-images.githubusercontent.com/43868540/84564061-1ad62780-ad9b-11ea-862f-9ca9563e6c57.png)

동작원리로는 
1. 서비스 요청자가 SOAP로 인코딩하여 웹 서비스 요청을 서비스 제공자에게 전달한다.
2. 서비스 제공자는 이를 디코딩하여 적절한 서비스 로직을 수행시켜서 결과를 얻는다.
3. 로직을 수행시켜서 얻은 결과를 SOAP로 인코딩하여 반환한다. 

여기서 WSDL과 UDDI의 개념이 모호할텐데 쉽게 WSDL은 xml이고, UDDI는 일종의 검색 엔진이라고 생각하면 된다.

그렇다면 인코딩을 위한 SOAP의 메시지 구조를 한번 살펴보자.

![SOAP 메시지 구조](https://user-images.githubusercontent.com/43868540/84564122-a780e580-ad9b-11ea-9f6d-e4803e1c9a6e.jpeg)
크게 HTTP Header와 SOAP part, Attachment 3개로 나뉘어 진다.

![SOAP Part](https://user-images.githubusercontent.com/43868540/84564083-4e18b680-ad9b-11ea-8bbf-b9fd71ec8bf2.png)
SOAP Part안에는 위의 사진처럼 xml형태로 데이터가 들어가 있다. 
SOAP 봉투(envelope), SOAP 헤더(header), SOAP 바디(body)로 구성된 하나의 xml문서로 표현된다. 이러한 복잡한 구성으로 인해 HTTP상에서 전달되기 무섭고, 메시지 인코딩/디코딩 과정 등 웹 서비스 개발의 난이도가 높아 개발 환경의 지원이 필요하다. 


#### Reference
[SOAP vs REST](http://blog.wishket.com/soap-api-vs-rest-api-두-방식의-가장-큰-차이점은/)
[SOAP](https://mygumi.tistory.com/55)
[SOAP 구조])(https://www.slideshare.net/yjaeseok/soap-rest)
[SOAP동작원리 이미지](https://devkingdom.tistory.com/12)
[SOAP 메시지](https://mygumi.tistory.com/55)
[SOAP동작원리 이미지](https://devkingdom.tistory.com/12)
