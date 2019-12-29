## appServlet/servlet-context.xml ERROR

appServlet/servlet-context.xml에서

<context:component-scan base-package="kr.co.study" />

->

<context:component-scan base-package="kr.co.controller" />

로 변경하니 500에러가 발생

### 해결 방법
```
spring이 Bean을 등록할때 클래스를 검색해서 클래스에 특정 어노테이션(@Controller, @Service, @Repository, @Component 등)이 붙어 있으면 이를 Spring Bean 클래스라고 인식하고 등록하게 된다.

이때 클래스를 검색하는 기능이 저 component-scan 인데 base-package에 명시된 package를 기준으로 해서 그 하위를 검색하는 것

하지만 controller를 기준으로 클래스를 검색하면 지금 구조에서는 HomeController 클래스 하나만 Spring Bean 클래스로 등록되고 다른 클래스들은 검색 기능으로 인한 등록이 되질 않음

그렇기 때문에 TestService를 주입받고 싶어도 그 클래스가 Spring Bean으로 등록이 되어 있지 않기 때문에 주입을 못받아서 에러가 발생

이 부분을 그래서 다음과 같이 고쳐야 함.

<context:component-scan base-package="com.comtrue" />
이렇게 하면 comtrue 밑에서부터 검색하기 때문에 그 하위 패키지은 controller 패키지는 물론 service 패키지도 포함해서 검색하는 것!!!

Spring에서 Bean 주입을 받을려면 주입 받고자 하는 Bean 도 Spring 에 등록되어 있어야 함.

```
