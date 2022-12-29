> index
> 

---

# 📌 스프링 프레임워크란?

## **Spring Framework의 특징**

- Java 플랫폼을 위한 오픈소스 애플리케이션 프레임워크
- 엔터프라이즈 급 애플리케이션을 만들기위한 모든 기능을 종합적으로 제공하는 경량화된 솔루션
- 동적인 웹사이트를 개발하기 위한 여러가지 서비스를 제공
- 대한민국 공공기관의 웹서비스 개발 시 사용을 권장하고 있는 전자정부 표준 프레임워크의 기반 기술로서 쓰이고 있다.
- 기본 뼈대를 흔들지 않고 다른 프레임워크를 혼용해서 사용할 수 있다.
- JEE (Java Enterprise Edition)가 제공하는 다수의 기능을 지원
- DI, AOP 지원
- 개발자가 복잡하고 실수하기 쉬운 Low Level에 신경쓰지 않고 Business Logic 개발에 전념할 수 있도록 해준다.

- 프레임워크 (Framework)
    
    ---
    
    개발할 때 설계 기본이 되는 뼈대나 구조 / 환경 (문제 영역을 해결한 재사용, 확장 가능한 라이브러리.)
    

### 🤜 POJO (Plain Old Java Object) 기반의 구성

<aside>
💡 스프링은 내부적으로 별도의 API를 사용하지 않고, 일반적인 Java 코드를 이용하여 객체를 구성하는 방식 그대로 사용하고 있다. 
→ 코드를 개발할 때, 개발자가 특정한 라이브러리나 컨테이너의 기술에 종속적이지 않다.

</aside>

- POJO
    - 특정 프레임워크나 기술에 의존적이지 않은 자바 객체
    - 특정 기술에 종속적이지 않기 때문에 생산성, 이식성 향상
    - `Plain` : component interface를 상속받지 않는 특징 (특정 framework에 종속되지 않는)
    - `Old` : EJB 이전의 java class를 의미
- 스프링에서 생성되어 관리되는 POJO 기반의 객체를  `Spring Bean`이라고 한다.
- 여기서 POJO는 단순 `getter/setter` 만으로 구성되어 있으며 단순히 new를 통해서 생성 가능한 형태를 말한다.
- 핵심은 특정 기술에 종속되는 어떤 클래스도 상속하지 않고 있으며 어떠한 인터페이스도 구현하고 있지 않은 자바 클래스이다.
- **잠깐 예시 code를 봐볼까요?**
    
    ---
    
    > POJO 개념을 사용하지 않았을 경우
    > 
    
    ---
    
    ```java
    public class ExampleListener implements MessageListener {
    
      public void onMessage(Message message) {
        if (message instanceof TextMessage) {
          try {
            System.out.println(((TextMessage) message).getText());
          }
          catch (JMSException ex) {
            throw new RuntimeException(ex);
          }
        }
        else {
          throw new IllegalArgumentException("Message must be of type TextMessage");
        }
      }
    
    }
    ```
    
    > POJO 개념을 사용한 경우
    > 
    
    ---
    
    ```java
    @Component
    public class ExampleListener {
    
      @JmsListener(destination = "myDestination")
      public void processOrder(String message) {
        System.out.println(message);
      }
    }
    ```
    
    이런 식으로 코드를 작성하게 되면 해당 클래스와의 결합도가 낮아져 다른 솔루션으로 변경하려고 할 때, @JmsListener를 다른 솔루션으로 코드수정하면 되므로, 유지보수에 있어서 좀 더 유용하게 활용할 수 있다.
    
    > ref
    > 
    
    ---
    
    [Spring의 기본 특징-POJO](https://velog.io/@galaxy/Spring%EC%9D%98-%EA%B8%B0%EB%B3%B8-%ED%8A%B9%EC%A7%95-POJO)
    

### 🤜 PSA (Portable Service Abstraction)

<aside>
💡 환경과 세부기술의 변경과 관계없이 일관된 방식으로 기술에 접근할 수 있는 환경을 제공해주는 설계원칙

</aside>

- 트랜잭션 추상화, OXM 추상화, 데이터 엑세스의 Exception 변환긴으 등 기술적인 복잡함은 추상화를 통해 Low Level의 기술 구현 부분과 기수을 사용하는 인터페이스로 분리
- 예를 들어 데이터베이스에 관계없이 동일하게 적용할 수 있는 트랜잭션 처리방식
- 대표적인 추상화의 예
    - JPA의 구현체(`Hibernate`, `Eclipse Link`)를 추상화하는 `Spring Data JPA`
    - `Mybatis`를 추상화하는 `Spring-mybatis`
    - `Spring Transaction Manager`, `Spring Cache Manager`
    - 서비스가 구동되는 환경(`Web MVC`, `Web Flux`)에 대해서도 추상화를 지원한다.
- 버전에 따라서 라이브러리 혹은 프레임워크의 내부 API의 설계나 인터페이스가 달라지더라도, `Sping`에서 적절히 감싸 추상화를 하기 때문에 우리의 소스코드는 변경될 일이 없다.

### 🤜 트랜잭션의 지원 (트랜잭션 처리를 위한 일관된 방법을 제공)

- JDBC, JTA 또는 컨테이너가 제공하는 트랜잭션을 사용하든, 설정 파일을 통해 트랜잭션 관련정보를 입력하기 때문에 트랜잭션 구현에 상관없이 동일한 코드를 여러 환경에서 사용이 가능
- 상황에 따라 여러 코드를 작업해줘야 하는데, 스프링에서는 Annotation이나 xml로 설정할 수 있도록 지원
- 추상화된 트랜잭션 관리를 지원하며 설정파일(xml, java, property 등)을 이용한 선언적인 방식 및 프로그래밍을 통한 방식을 모두 지원한다.

### 🤜 영속성과 관련된 다양한 API를 지원

- 스프링은 JDBC를 비롯하여 iBatis, MyBatis, Hibernate, JPA 등 DBA처리를 위해 널리 사용되는 라이브러리와 연동을 지원

### 🤜 다양한 API에 대한 연동을 지원

- JMS, 메일, 스케쥴링 등 엔터프라이즈 어플리케이션 개발에 필요한 다양한 API를 설정 파일과 어노테이션을 통해서 손쉽게 사용할 수 있도록 지원

### 🤜 DI (Dependency Injection) _ 의존성 주입

- 유연하게 확장 가능한 객체를 만들어 두고 객체 간의 의존관계는 외부에서 다이나믹하게 설정
- 각각의 계층이나 서비스들 간에 의존성이 존재할 경우, 프레임워크가 서로 연결시켜준다.
- 스프링은 설정 파일(xml, java)이나, 어노테이션을 통해서 객체 간의 의존 관계를 설정할 수 있다.
- 객체는 의존하고 있는 객체를 직접 생성하거나 검색할 필요가 없다.
- ApplicationContext라는 존재가 필요한 객체들을 생성하고 필요한 객체들을 주입하는 역할을 해주는 구조
    
    따라서 스프링을 사용하면 객체와 객체를 분리해서 생성하고 이런 객체들을 엮는 작업을 하게 된다. (Wiring)
    
    ApplicationContext가 관리하는 객체들을 `Bean` 이라고 부르고, 빈과 빈 사이의 의존관계를 처리하는 방식으로, xml, Annotation, Java 등 다양한 방식이 사용된다.
    
    > xml
    > 
    
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="..">
    
    <context:component-scan base-package="com.ssafy"/>
    
    <bean id="dataSource" class="org.springframework.">
    	<property name="driverClass" value="com.mysql....."/>
    	<property name="url" value="jdbc:mysql://127.,,"/>
    	<property name="username" value="ssafy">
    	<property name="password" value="ssafy"/>
    </bean>
    ```
    
    > annotation
    > 
    
    ```java
    @Repository
    public class BoardDaoImpl implements BoardDao {
    
    	private final DataSource dataSource;
    	private final DBUtil dbUtil;
    	
    	@Autowired
    	public BoardDaoImpl(DataSource dataSource, DBUtil dbUtil) {
    		this.dataSource = dataSource;
    		this.dbUtil = dbUtil;
    	}
    ...
    }
    ```
    
    > java
    > 
    
    ```java
    package com.ssafy.configuration;
    
    import javax.sql.DataSource;
    
    @Configuration
    @ComponentScan(basePackages = {"com.ssafy"})
    public class ApplicationConfig {
    
    	@Bean
    	public DataSource getDataSource(){
    		SimpleDriverDataSource sdds = new SimpleDriverDataSource();
    		sdds.set ...
    		...
    		sdds.setPassword("ssafy");
    		return sdds;
    	}
    }
    ```
    

### 🤜 IoC (Invertion of Control) _ 제어 역행

<aside>
💡 제어권이 `사용자`가 아니라 `프레임워크`에 있어 필요에 따라 스프링에서 사용자 코드 호출

</aside>

- 애플리케이션의 느슨한 결합을 도모
- 컨트롤의 제어권이 사용자가 아니라 프레임워크에 있어 필요에 따라 스프링에서 사용자의 코드를 호출
- 객체 생성을 Container에게 위임하여 처리
- interface로 생성? 호출하는것도 IoC의 방법이였다! `AS`
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/468a32f0-74a9-4b2d-828f-086491e2d64c/Untitled.png)
    

### 🤜 AOP (Aspect Oriented Programming) _ 관점지향 프로그래밍

<aside>
💡 공통적으로 사용하는 기능의 경우 해당 기능을 분리하여 관리

</aside>

- AOP : 문제를 바라보는 관점을 기준으로 프로그래밍 하는 기법
- 트랜잭션이나 로깅, 보안과 같이 여러 모듈에서 공통적으로 사용하는 기능의 경우 해당 기능을 분리하여 관리할 수 있다.
- 관심사의 분리를 통해서 소프트웨어의 모듈성을 향상
- 공통 모듈을 여러 코드에 쉽게 적용 가능
- 이해가 잘 안된다면?
    
    ---
    
    > 공통 관심 사항 vs 핵심 관심 사항
    > 
    
    ---
    
    공통 관심사항 : 비즈니스 로직은 아니지만, 보안, 로그, 트랜잭션과 같이 반드시 처리가 필요한 부분 → AOP가 해결해줌!
    
    AOP로 활용할 객체에는 `@Aspect` 어노테이션을 붙여줘야 한다.
    
    [우리는 왜 스프링을 사용하는가? - Java spring의 특징](https://joychae.tistory.com/27)
    

### 스프링 모듈

### 📍 Spring Core

- Spring 프레임워크의 근간이 되는요소. IoC(또는 DI) 기능을 지원하는 영역을 담당.
- BeanFactory를 기반으로 Bean 클래스들을 제어할 수 있는 기능을 지원

### 📍 Spring Context

- Spring Core 바로 위에 있으면서 Spring Core에서 지원하는 기능외에 추가적인 기능들과 좀 더 쉬운 개발이 가능하도록 지원

- 또한 JNDI, EJB등을 위한 Adaptor들을 포함

### 📍 Spring DAO

- 지금까지 우리들이 일반적으로 많이 사용해왔던 JDBC 기반하의 DAO개발을 좀 더 쉽고, 일관된 방법으로 개발하는 것이 가능하도록 지원

- Spring DAO를 이용할 경우 지금까지 개발하던 DAO보다 적은 코드와 쉬운 방법으로 DAO를 개발하는 것이 가능

### 📍 Spring ORM

- Object Relation Mapping 프레임워크인 Hibernate, IBatis, JDO와의 결합을 지원하기 위한 기능

- Spring ORM을 이용할 경우 Hibernate, IBatis, JDO 프레임워크와 쉽게 통합하는 것이 가능

### 📍 Spring AOP

- Spring 프레임워크에 Aspect Oriented Programming을 지원하는 기능이다. 이 기능은 AOP Alliance 기반하에서 개발
- 설정 관리 기능을 통해 AOP 기능을 Spring 프레임워크와 직접 통합 시킨다.

### 📍 Spring Web

- Web Application 개발에 필요한 Web Application Context와 Multipart Request등의 기능을 지원

- 또한 Struts, Webwork와 같은 프레임워크의 통합을 지원하는 부분을 담당

### 📍 Spring Web MVC

- Spring 프레임워크에서 독립적으로 Web UI Layer에 Model-View-Controller를 지원하기 위한 기능

지금까지 Struts, Webwork가 담당했던 기능들을 Spring Web MVC를 이용하여 대체하는 것이 가능하다. 또한 Velocity, Excel, PDF와 같은 다양한 UI 기술들을 사용하기 위한 API를 제공

# ***예상 면접 질문 및 답변***

---

### ***IoC 컨테이너란?***

스프링 애플리케이션에서는 객체(빈)의 생성과 관계설정, 사용, 제거 등의 작업을 애플리케이션 코드 대신 스프링 컨테이너가 담당하는데, 이를 IoC 컨테이너라고 한다.

### ***IoC 컨테이너의 장점은?***

스프링 애플리케이션의 객체(빈)을 IoC 컨테이터가 관리해줌으로써 개발자의 부담이 줄고 비즈니스 로직에 더욱 집중할 수 있다는 장점이 있다.

### ***DI란?***

DI는 객체(빈)들 간의 의존관계를 외부에서 결정하고 주입하는 것이다.

`BurgerChef` 클래스와 `BurgerRecipe` 인터페이스를 예시로 설명하자.

### ***DI의 장점은?***

- 의존성이 줄어든다.
    - 의존한다는 것은 그 의존대상의 변화에 취약하다는 것이다.(대상이 변화하였을 때, 이에 맞게 수정해야함)
    - DI로 구현하게 되었을 때, 주입받는 대상이 변하더라도 그 구현 자체를 수정할 일이 없거나 줄어들게된다.
- 재사용성이 높은 코드가 된다.
    - 기존에 BurgerChef 내부에서만 사용되었던 BurgerRecipe을 별도로 구분하여 구현하면, 다른 클래스에서 재사용할 수가 있다.
- 테스트하기 좋은 코드가 된다.
    - BurgerRecipe의 테스트를 BurgerChef 테스트와 분리하여 진행할 수 있다.
- 가독성이 높아진다.
    - BurgerRecipe의 기능들을 별도로 분리하게 되어 자연스레 가동성이 높아진다.

### ***DI의 종류는?***

DI는 생성자 삽입, 수정자 삽입, 필드 주입이 있다.

생성자 주입은 생성자 호출시점에 딱 1번만 호출되는 것을 보장하며 불변, 필수 의존관계에 사용한다.

수정자 주입은 선택, 변경 가능성이 있는 의존관계에 사용되며 빈을 선택적으로 주입이 가능하다.

필드 주입은 외부에서 변경이 불가능하여 테스트 하기 힘들다. DI 프레임워크 없이는 작동하기 힘들며, 주로 애플리케이션과 관계없는 테스트코드나 @Configuration 같은 스프링 설정 목적으로 사용한다.

### ***순환 참조가 무엇이고 언제 발생하는가?***

순환 참조란 서로 다른 여러 빈들이 서로를 참조하고 있음을 의미한다. 필드 주입이나 수정자 주입은 객체 생성 후 비즈니스 로직 상에서 순환 참조가 일어나기 때문에 컴파일 단계에서 순환 참조를 잡아낼 수 없다. 반면에 생성자 주입을 사용하면 스프링 컨테이너가 빈을 생성하는 시점에 순환 참조를 확인하기 때문에 컴파일 단계에서 순환 참조를 잡아낼 수 있다

### ***생성자 주입을 사용해야 하는 이유는?***

- 의존관계를 모두 주입하지 않은 경우에 객체를 생성할 수 없기 때문에 NPE가 발생하지 않는다.
- `final` 키워드를 사용할 수 있어 불변성을 보장할 수 있다.
- 생성자 주입은 컴파일 단계에서 순환 참조를 잡아 낼 수 있다.
- 의존성을 주입하기 번거롭고 생성자 인자가 많아지면 코드가 길어져 위기감을 느낄 수 있다. 이를 바탕으로 SRP 원칙을 생각하게 되고, 리팩토링을 하게 된다.
- DI 컨테이너 없이 직접 의존성을 주입할 수 있다.

### ***Spring IoC/DI의 동작 과정은?***

IoC(제어의 역전)은 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것으로 코드의 최종 호출은 개발자가 제어하는 것이 아닌 프레임워크의 내부에서 결정된 대로 이루어진다.

DI(의존관계 주입)은 스프링 프레임워크에서 지원하는 IoC의 형태로 객체(빈) 사이의 의존관계를 빈 설정 정보를 바탕으로 DI 컨테이너가 자동으로 연결한다.

### ***Autowiring 동작 과정은?***

스프링 서버가 올라갈 때 애플리케이션 컨텍스트가 @Bean이나 @Service, @Controller 등 어노테이션을 이용하여 등록한 스프링 빈을 생성하고, @Autowired 어노테이션이 붙은 위치 또는 생성자, 수정자를 통해 주입한다.

### ***DI와 IoC의 차이는?***

DI는 의존관계를 어떻게 가질 것인가에 대한 문제고, IoC는 누가 소프트웨어의 제어권을 갖고 있느냐의 문제다. IoC 컨테이너가 빈을 생성할 때 빈들간의 의존관계를 DI를 통해 해결한다.

DI는 IoC 사용을 필수로 요구하지 않는다는 점을 주의해야 한다.

# 📌 Spring, Spring MVC, Spring Boot의 차이

### 🤜 Spring MVC

> M(모델)
> 
- 평범한 자바 객체
- 도메인 객체 또는 DTO로 화면에 전달할 또는 화면에서 전달 받은 데이터를 담고 있는 객체

> V(뷰)
> 
- HTML, JSP, 타임리프..
- 데이터를 보여주는 역할. 다양한 형태로 보여줄 수 있음 (HTML, JSON, XML)\

> C(컨트롤러)
> 
- 스프팅 @MVC
- 사용자의 입력을 받아 모델 객체의 데이터를 변경하거나, 모델 객체를 뷰에 전달
- 입력 값 검증, 입력 받은 데이터를 모델 객체로 변경, 변경된 모델 객체를 뷰에 전달

### 👀 Spring MVC 동작원리

> **전체 흐름**
요청 → 프론트 컨트롤러 → 핸들러 매핑 → 핸들러 어댑터 → 커늩롤러 → 로직 수행 → 컨트롤러 → 뷰 리졸버 → 응답
> 

---

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/284af48b-5dc9-461c-834e-d955c1568812/Untitled.png)

1. 요청된 URL을 dispatcher-servlet으로 전달.
2. 핸들러 매핑은 해당 URL에 매핑된 컨트롤러가 있는지 검사 후 컨트롤러에 전달.
3. 해당 컨트롤러가 로직을 처리.
4. ModelAndView 객체 생성 후, 로직의 결과를 담아서 dispatcher-servlet에 전달.
5. dispatcher-servlet은 전달 받은 뷰가 있는지 검사하기 위해 ViewResolver로 보냄.
6. ViewResolver는 받은 뷰가 있는지 검사 후 뷰로 보냄.
7. 모델과 같이 뷰를 그린 후에 dispatcher-servlet으로 보냄.
8. 최종적으로 컨텐츠를 클라이언트에게 전달.

### 🤜 Spring Boot

Spring Framework 기반 (기존 Spring 위에 구축)

- 스프링의 모든 기능을 제공하면서 **보다 쉽게 사용 가능**
    - 개발에 필요한 모듈의 라이브러리 조합이 자동으로 되어있음
- 모든 것이 자동으로 구성
    - Spring Framework는 Bean으로 등록해주어야 하지만, Spring Boot는 의존성만 추가해준다면 yml파일을 동해 자동으로 주입시켜 설정해줌
- 마이크로 서비스 기반 프레임 워크 (짧은 시간 내에 프로덕션 준비 애플리케이션 생성)
- **REST API**를 이용하여 개발 시 유용하게 사용 가능
- war, jar 파일로 변환하는 기능 제공
- 자주 사용하는 라이브러리가 미리 조합되어 있음
- 복잡한 설정이 자동 처리
- 내장서버를 포함(톰캣)하여 별도로 웹서버를 추가하지 않아도 바로 개발 가능
- WAS에 배포하지 않고도 실행 가능한 jar 파일로 웹앱 개발 가능

### 👀 SpringBoot의 Spring과의 차이점

- Embed Tomcat을 사용하기 때문에, (Spring Boot 내부에 Tomcat이 포함되어있다.) 따로 Tomcat을 설치하거나 매번 버전을 관리해 주어야 하는 수고로움을 덜어준다.
- **starter을 통한 Dependency 자동화**
    
    과거 Spring framework에서는 각각의 dependency들의 호환되는 버전을 일일이 맞추어 주어야 했고, 때문에 하나의 버전을 올리고자 하면 다른 dependeny에 까지 영향을 미쳐 version 관리에 어려움이 많았다. 하지만, 이제 starter가 대부분의 dependency를 관리해주기 때문에 이러한 걱정을 많이 덜게 되었다.
    
- **Configuration**
    
    Spring은 configuration 설정을 할 때 매우 길고, 모든 어노테이션 및 빈 등록 등을 설정해줘야한다.
    SpringBoot는 application.properties 파일이나 application.yml파일에 설정하면 된다.
    
- XML설정을 하지 않아도 된다.
- **편리한 배포**
    
    Spring은 war 파일을 Web Application Server에 담아 배포했지만,
    
    SpringBoot는 jar 파일을 이용해 자바 옵션만으로 손쉽게 배포가 가능하다. Spring Actuaor를 이용한 애플리케이션의 모니터링과 관리를 제공한다.
    (내장 서버를 포함해서 tomcat과 같은 WAS를 추가로 설치하지 않아도 개발 가능)
    (WAS에 배포하지 않고도 실행할 수 있는 JAR파일로 WebApplication을 개발 가능)
    

---

### 정리

- **Spring**
    
    **`Java 기반의 웹 애플리케이션 개발을 위한 오픈소스 프레임워크`**
    
- **Spring MVC**
    
    **`웹 애플리케이션 개발에 있어 MVC 패턴을 적용할 수 있도록 Spring에서 제공하는 프레임워크`**
    
- **Spring Boot**
    
    **`Spring 설정들을 자동화하는 Spring 기반의 프레임워크`**
    

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/018dbef4-5062-4f56-a4d1-83b10d56979d/Untitled.png)

> ref.
> 

spring framework의 특징 및 정의 

[Spring MVC](https://velog.io/@koseungbin/Spring-MVC)

[스프링 프레임워크의 장,단점 및 특징](https://velog.io/@whitecloud94/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%EC%9D%98-%EC%9E%A5%EB%8B%A8%EC%A0%90-%EB%B0%8F-%ED%8A%B9%EC%A7%95)

[[Spring] 스프링(Spring) 정의 및 특징 정리](https://goddaehee.tistory.com/156)

[스프링의 세 가지 특징](https://dongwooklee96.github.io/post/2021/03/10/%EC%8A%A4%ED%94%84%EB%A7%81%EC%9D%98-%EC%84%B8-%EA%B0%80%EC%A7%80-%ED%8A%B9%EC%A7%95/)

[[Spring] Spring Framework 스프링 정의 및 특징](https://truecode-95.tistory.com/7)

[우리는 왜 스프링을 사용하는가? - Java spring의 특징](https://joychae.tistory.com/27)

Spring MVC, Boot

[Spring Boot vs. Spring MVC vs. Spring 의 비교](https://m.blog.naver.com/sthwin/221271008423)

[Spring? Spring Boot? Spring MVC?](https://it-hhhj2.tistory.com/97)

[스프링 vs 스프링부트 차이점 10분만에 이해하기](https://incomeplus.tistory.com/344)

[Spring MVC vs Spring Boot](https://velog.io/@hellonayeon/springmvc-vs-springboot)

[Spring 과 Spring Boot 차이](https://velog.io/@courage331/Spring-%EA%B3%BC-Spring-Boot-%EC%B0%A8%EC%9D%B4)