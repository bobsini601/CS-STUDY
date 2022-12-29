> index
> 

<aside>
‼️ Bean, Container, DI 는 유기적으로 연관되어있습니다!
그래서 제 설명들이 짬뽕이 되어있을 수 있습니다..!
여튼 발표 시작해보겠습니다아

</aside>

# 📌 Bean

<aside>
💡 스프링 IoC 컨테이너에 의해 관리되는 자바 객체(POJO)

</aside>

- 스프링이 직접 그 생성과 제어를 담당하는 오브젝트만을 Bean이라고 부른다.

- xml 설정 파일이나, java 설정 파일에 bean을 정의해주면 해당 설정 파일을 이용해 스프링 컨테이너를 생성한 다음에 컨테이너가 Bean 정의 내용대로 Bean을 관리하도록 한다.
    
    ```java
    @Configuration
    public class SpringConfig {
    	...
    	...
    	@Bean
    	public MemberService memberService(){
    		return new MemberService(memberRepository());
    	}
    	@Bean
    	public MemberRepository memberRepositry() {
    		return new MemoryMemberRepository();
    	}
    }
    ```
    
    ```xml
    <beans ...>
    	...
    	<bean id="memberDao" class="com.test.hello.dao.MemberDaoImpl" />
    	<bean id="memberService" class="com.test.hello.service.MemberServiceImpl" scope="prototype" />
    		<property name="memberDao" ref="memberDao"/>
    	</bean>
    <beans/>
    ```
    

## 🪧 Bean 등록하는 방법

### ✒️ xml

<aside>
💡 등록하려는 객체를 xml에 설정한다.

</aside>

![applicationContext.xml](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/190d761e-f449-4344-aed1-770a6fb6e1d6/Untitled.png)

applicationContext.xml

코드에서 Service 내부에 Dao가 존재하기 떄문에 property로 Dao를 등록한 것이다! 

- root tag는 `<beans>`
- `<bean>`  : 스프링 컨테이너가 관리할 Bean 객체를 설정
    - id : 주입 받을 곳에서 호출할 이름 설정 (유일 값)
    - class: 주입할 객체 클래스
    - factory-method : Singleton 패턴으로 작성된 객체의 factory 메소드 호출

### ✒️ Annotation

```java
@Component
public class MemberServiceImpl implemnts MemberService {

	@Autowired
	private MemberDao memberDao;

	@Override
	public int registMember (MemberDto memberDto) {
		return memberDao.registerMember(memberDto);
	}
}
```

- 빈으로 사용될 클래스에 Annotation을 부여해 주면 자동으로 빈 등록 가능
- 어플리케이션의 규모가 커지고 빈의 개수가 많아질 경우 xml파일을 관리하는 것이 번거로움
- Annotation으로 빈을 설정할 경우 반드시 component-scan을 설정해야 한다
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a1aae287-7727-4651-abc9-e00b73c42345/Untitled.png)
    

> Stereotype Annotation 종류
> 

---

- 빈 자동 등록에 사용할 수 있는 annotation 4가지

| Stereotype | 적용 대상 |
| --- | --- |
| @Repository | DAO 또는 Repository 클래스에 사용 |
| @Service | Service 클래스에 사용 |
| @Controller | MVC Controller 에 사용
스프링 웹 서블릿에 의해 웹 요청을 처리하는 컨트롤러 빈으로 설정 |
| @Component | 위의 Layer 구분을 적용하기 어려운 일반적인 경우에 설정 (ex. DBUtil)
** @Repository, @Service,  @Controller 중에 뭘 해야할 지 모르겠다! 하면 @Component ** |
- @Configuration
    - 스프링 설정 정보로 인식하고 스프링 빈이 **싱글톤**을 유지하도록 추가 처리를 한다. (물론 스프링 빈 스코프가 싱글톤이 아니라면 추가 처리를 하지 않음.)
- @Bean
    
    내가 직접 작성한 클래스가 아니라 외부 라이브러리의 객체를 빈으로 만들고 싶을 때 사용
    
    외부 라이브러리의 클래스에 Annotation을 직접 붙일 수는 없으니 다음과 같이 객체를 반환하는 메서드에 붙여서 사용
    

## 🪧 Bean의 생명주기(Life Cycle)

<aside>
💡 스프링 IoC 컨테이너 생성 -> 빈 생성 -> 의존관계 주입 -> 초기화 콜백 -> 사용 -> 소멸전 콜백의 생명주기를 가진다.

</aside>

![singleton bean의 생명주기](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5ebb51d5-f7b3-446c-ba93-7c7453310ca9/Untitled.png)

singleton bean의 생명주기

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ef67525d-599d-4bbd-a647-9d9e990c5b79/Untitled.png)

## 🪧 Bean의 생성범위(scope)

<aside>
💡 해당 객체가 어디까지 영향을 미치는 가를 결정하는 부분

</aside>

> default - 싱글톤 빈 (Singleton Bean)
> 

---

- 스프링 빈은 기본적으로 싱글톤으로 만들어짐
- 그러므로, 컨테이너가 제공하는 모든 빈의 인스턴스는 항상 동일함
- 컨테이너가 항상 인스턴스를 반환하게 만들고 싶은 경우 scope를 prototype으로 설정해야함
    
    ```xml
    <bean id="memberService" class="com.ssafy.board.model.service.BoardServiceImpl" scope="prototype"/>
    ```
    

> 빈의 생성 범위 지정
> 

---

| scope | 내용 |
| --- | --- |
| singleton | 스프링 컨테이너당 하나의 인스턴스 빈만 생성 (default) |
| prototype | 컨테이너 빈을 요청할 때마다 새로운 인스턴스 생성 |
| request(web scope) | HTTP Request별로 새로운 인스턴스 생성,
HTTP Request 요청하나가 들어오고 나갈 때까지 유지되는 스코프, 각각의 HTTP 요청마다 별도의 인스턴스가 생성되고 관리 |
| session(web scope) | HTTP Session별로 새로운 인스턴스 생성,
HTTP Session과 동일한 생명주기를 가지는 스코프 |
| application(web scope) | 웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지 스코프 |
| websocket(web scope) | 웹 소켓과 동일한 생명주기를 가지는 스코프 |
| global session | 하나의 빈 정의에 대해 global session 생명주기 안에 하나의 객체가 존재, 포틀릿 기반의 웹 애플리케이션 용도로 전역 세션 스코프가 빈과 같은 스프링 MVC를 사용한 포탈 애플리케이션 내의 모든 포틀릿 사이에 공유 |
| thread | 새 스레드에서 요청하면 새로운 bean 인스턴스를 생성. 같은 스레드의 요청에는 항상 같은 인스턴스가 반환 |
| custom | org.pringframework.beans.factory.config.Scope를 구현하고 커스텀 스코프를 스프링의 설정에 등록하여 사용 |

# 📌 Container (Spring IoC Container)

<aside>
💡 Bean을 관리하는 객체

</aside>

### 🪧 Container 란?

- 객체(Bean)의 생성, 사용, 소멸에 해당하는 라이프사이클을 담당
- 라이프사이클을 기본으로 애플리케이션 사용에 필요한 주요 기능을 제공

### 🪧 Container 기능

- 라이프사이클 관리
- Dependency 객체 제공
- Thread 관리
- 기타 애플리케이션 실행에 필요한 환경

### 🪧 Container의 필요성

- 비즈니스 로직외에 부가적인 기능들에 대해서는 독립적으로 관리되도록 하기 위함
    
    <aside>
    ‼️ (DI의 특징과 연관)
    
    개발자가 객체를 new해서 생성하지않고, Ioc컨테이너에 존재하는 Bean 객체를 주입해준다. 해당 기능을 사용하면 싱글톤, 개발자의 편의, 성능 이슈 등등을 해결해준다.
    
    </aside>
    
- 서비스 lookup이나 Configuration에 대한 일관성을 갖기 위함
- 서비스 객체를 사용하기 위해 각각 Factory 또는 Singleton 패턴을 직접 구현하지 않아도 됨

## 🪧 IoC Container

<aside>
‼️ 저희가 컨테이너를 IoC 컨테이너라고 부르는데요.
오브젝트(빈)의 생성과 관계설정, 사용, 제거 와 같은 작업들을 사용자가 관리하는 것이 아니라 컨테이너가 담당하기 때문에, (이게 바로 IoC _제어의 역전) 이렇게 부릅니다.

</aside>

> 제어의 역전이란, 객체의 생성 및 생명주기에 대한 모든 객체에 대한 제어권이 바뀌었다는 것을 의미한다.
> 
- 오브젝트의 생성과 관계설정, 사용, 제거 등의 작업을 애플리케이션 코드 대신 독립된 컨테이너가 담당
- 컨테이너가 코드 대신 오브젝트에 대한 제어권을 갖고있어 IoC라고 부름
- 이런 이유로, 스프링 컨테이너를 IoC라고 부르기도 함
- 스프링에서 IoC를 담당하는 컨테이너에는 `BeanFactory` , `ApplicationContext` 가 있음

### 📍 IoC 컨테이너 Class (BeanFactory, ApplicationContext)

- org.springframework.context.`**ApplicationonContext**` 인터페이스가 대표적.
    
    
    > 애플리케이션 컨텍스트 (ApplicationContext)
    > 
    
    ---
    
    - BeanFactory를 **확장**한 IoC 컨테이너이다.
    - Bean을 등록하고 관리하는 기본적인 기능은 BeanFactory와 동일하다.
    - 스프링이 제공하는 각종 부가 서비스를 추가로 제공한다.
    
    > 빈 팩토리 (BeanFactory)
    > 
    
    ---
    
    - 스프링이 IoC를 담당하는 핵심 컨테이너
    - Bean을 등록/생성/조회/반환 기능을 담당
    - 일반적으로 BeanFacrtory를 사용하지 않고 이를 확장한 ApplicationContext를 이용
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d63ec69-050c-4229-b636-6e67c6780636/Untitled.png)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/704d0d9b-c31e-45f3-8053-c873a602a3f7/Untitled.png)
    
    - BeanFactory라고 부를 때에는 주로 빈의 생성과 제어의 관점에서 이야기하는 것이고, ApplicationContext라고 할 때는 스프링이 제공하는 애플리케이션 지원 기능을 모두 포함해서 이야기하는 것이라고 보면 된다.

> 스프링 IoC 컨테이너가 왜 Bean을 관리할까?
> 

---

- 의존성을 사용하는 로직에만 집중 가능
- 의존성이 주입 될 객체가 싱글 오브젝트임을 보장

# 📌 DI (Dependency Injection) _ 의존성 주입

- 유연하게 확장 가능한 객체를 만들어 두고 객체 간의 의존관계는 외부에서 다이나믹하게 설정
- 각각의 계층이나 서비스들 간에 의존성이 존재할 경우, 프레임워크가 서로 연결시켜준다.
- 스프링은 설정 파일(xml, java)이나, 어노테이션을 통해서 객체 간의 의존 관계를 설정할 수 있다.

---

- 우리가 개발하는 애플리케이션은 레이어로 구별이되고, 각 레이어들은 단방향으로 의존성을 가지고 있다. (Controller → Service, Service → Repository)
- 의존성 주입을 사용하지 않을 경우, 개발자가 구현 객체를 직접 생성해서 의존성을 연결해주어야 한다.

```java
public class UserServiceImpl implements UserService {

    private UserRepositoryImpl userRepository = new UserRepositoryImpl();

    ....
}
```

- 그러나 이러한 방법은 **단위테스트 작성을 어렵게 만들고**, 두 레이어 구현체에 대한 **결합도를 높여 유지보수 비용을 불러일으킨다**.
- 인터페이스를 활용하여 두 구현체 간의 결합도를 낮추고, 연결의 책임을 스프링 프레임워크에 인계할 수 있다.

```java
public class UserServiceImpl implements UserService {

    @Autowired
    private UserRepository userRepository;

    ....
}
```

- 하지만 스프링이 관리할 수 있는 객체는 스프링 빈으로 등록된 객체만 가능하다.
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
    

## 🪧 DI의 장점

어떤 객체 참조를 static 변수 또는 내부 멤버 변수로 두는 것 대비, interface를 참조하여 DI를 받는 것은 다음과 같은 장점이 있다.

- 다형성을 사용할 수 있으니 프로그램이 유연해진다. → 결합도 낮아짐
- 별도 Configuration이 필요한 경우, 설정이 적용된 Bean을 각 서비스에서 DI를 받을 수 있음
- DI 주체인 외부 컨테이너에서 Singleton lifecycle을 관리해줄 수 있다. (eg, Spring Container의 Bean lifecycle 관리)

<aside>
‼️ 정리하는 느낌으로다가 가져와봤습니다.

</aside>

# 🔍 (추가) IoC 컨테이너의 DI를 통한 중재

![https://velog.velcdn.com/images%2Fjkijki12%2Fpost%2F7df46064-a75c-49de-a024-87e8572dc0b2%2Fimage.png](https://velog.velcdn.com/images%2Fjkijki12%2Fpost%2F7df46064-a75c-49de-a024-87e8572dc0b2%2Fimage.png)

구체적인 과정을 살펴보자!

1. Container가 로드되면, Bean에 해당하는 객체들을 scan 하여, 해당 Bean들을 생성하려고 한다.
2. 이 과정에서 의존성 주입이 이루어지게 되는데, 만약 순환 참조가 있다면 예외가 발생하여 Application은 종료된다.
3. 이제 Bean들이 생성되려고 하는데, 사용자가 지정한 init method가 존재한다면, 객체가 생성되고 init이 실행되게 된다.
4. 그 뒤에 사용자가 지정한 utility method(afterPropertiesSet)과 같은 메서드가 존재한다면, 해당 메서드가 실행되게 된다.(콜백 함수)
5. 프로그램이 종료되기 전에 이제 Container도 같이 종료되려고 하는데, 이 과정에서 destory 메서드가 존재한다면, 실행하고 정상적으로 종료 됩니다.

# CS 질문 list

---

### ***스프링 빈이란?***

스프링 빈은 스프링 컨테이너에 의해 관리되는 자바 객체(POJO)를 의미한다.

### ***스프링 컨테이너란?***

스프링 컨테이너는 스프링 빈의 생명 주기를 관리하며, 생성된 스프링 빈들에게 추가적인 기능을 제공하는 역할을 한다. IoC와 DI의 원리가 스프링 컨테이너에 적용된다.

### ***스프링 빈 등록 방식을 설명하라.***

클래스 위에 @Component를 붙인 후 ComponentScan을 이용하여 빈을 자동 등록하거나, @Configuration이 붙은 설정 파일 내의 특정 타입을 리턴하는 메소드 위에 @Bean을 붙여서 빈을 등록하는 방법이 있다.

### ***@Component vs @Bean***

- @Bean
    - 개발자가 컨트롤이 불가능한 **외부 라이브러리들을 Bean으로 등록하고 싶은 경우**에 사용된다.
    - 메소드 또는 어노테이션 단위에 붙일 수 있다.
- @Component
    - 개발자가 **직접 컨트롤이 가능한 클래스들의 경우**에 사용된다.
    - 클래스 또는 인터페이스 단위에 붙일 수 있다.

### ***@Configuration은 어떻게 싱글톤 빈을 보장하는가?***

클래스의 바이트 코드를 조작하는 CGLIB 라이브러리를 사용하여 싱글톤을 보장한다. CGLIB는 프록시 객체의 일종으로 설정 파일이 빈으로 등록될 때, 해당 설정 파일을 상속 받은 프록시 객체가 빈으로 등록된다. 그리고 설장 파일에서 @Bean이 붙은 메소드마다 이미 스프링 빈이 존재하면 존재하는 빈을 반환하고, 스프링 빈이 없으면 비로소 등록하고 반환하는 식으로 싱글톤을 보장한다.

### ***Bean Lite Mode가 무엇인가?***

Bean Lite Mode는 CGLIB를 이용하여 바이트 코드 조작을 하지 않는 방식을 의미한다. 이때 스프링 빈에 대해 싱글톤을 보장하지 않는다.

### ***스프링 빈 스코프에 대해 설명하라.***

스프링에서 Singleton과 Prototype 빈 스코프를 제공하고 있으며, 스프링 MVC 웹 애플리케이션을 사용할 경우 웹 스코프를 제공한다.

### ***Singleton 빈이란?***

- 싱글톤 빈은 스프링 컨테이너에서 한 번만 생성되며, 컨테이너가 사라질 때 제거된다.
- 생성된 하나의 인스턴스는 Spring Beans Cache에 저장되고, 해당 빈에 대한 요청과 참조가 있으며 캐시된 객체를 반환한다. 하나만 생성되기 때문에 동일 참조를 보장한다.
- 기본적으로 모든 빈은 스코프가 명시적으로 지정되지 않으면 싱글톤이다.

### ***Prototype 빈이란?***

- 프로토 타입 빈은 DI가 발생할 때마다 새로운 객체가 생성되어 주입된다.
- 빈 소멸에 스프링 컨테이너가 관여하지 않고, gc에 의해 빈이 제거된다.

### ***언제 Singleton 빈을 사용하고, 언제 Prototype 빈을 사용하는가?***

- 싱글톤 타입으로 적합한 객체
    - 상태가 없는 공유 객체
    - 읽기 전용으로만 상태를 가진 객체
    - 쓰기가 가능한 상태를 지니면서도 사용 빈도가 매우 높은 객체
        - 단, 이때는 동기화 전략이 필요함.
- 프로토 타입으로 적합한 객체
    - 사용할 때마다 상태가 달라져야 하는 객체
    - 쓰기가 가능한 상태가 있는 객체

### ***Singleton 빈과 Prototype 빈과 같이 사용할 때 어떤 문제가 생길 수 있는가?***

싱글톤 객체가 프로토 타입 객체를 가지고 있는 경우에는 의도한 것과 다른 결과를 낼 수도 있다. 이미 싱글톤 빈으로 생성되는 시점에 프로토 타입 빈이 생성되어 들어오기 때문에 싱글톤 빈 내부의 프로토 타입 빈을 호출하게 되면 매번 같은 값을 가져 온다.

### ***Singleton 빈 내부의 Prototype 빈을 사용할 때마다 다른 인스턴스를 받아오려면 어떻게 해야 하는가?***

Java.inject의 Provider를 사용하거나, 빈 스코프 설정에서 프록스 모드를 TAGET_CLASS로 설정하면 된다.

### ***웹 스코프가 무엇인가?***

웹 스코프는 웹 환경에서만 동작하는 스코프이며 프로토 타입과 다르게 특정 주기가 끝날 때까지 관리를 해 준다. 따라서 @PreDestory와 같은 소멸 콜백이 호출된다는 특징이 있다.

### ***웹 스코프의 종류는?***

- Request
    - HTTP 요청 하나가 들어오고 나갈 때까지 유지되는 스코프
    - 각각의 HTTP 요청마다 별도의 빈 인스턴스가 생성되고 관리된다.
- Session
    - HTTP Session과 동일한 생명 주기를 가지는 스코프
- Application
    - 서블릿 컨텍스트와 동일한 생명 주기를 가지는 스코프
- WebSocket
    - 웹 소켓과 동일한 생명 주기를 가지는 스코프

### ***Singleton 빈의 생명 주기를 설명하라.***

1. 스프링 컨테이너 생성
2. 스프링 빈 생성
3. 의존 관계 주입
4. 초기화 콜백
5. 사용
6. 소멸 전 콜백
7. 스프링 종료

### ***Prototype 빈의 생명 주기를 설명하라.***

1. 스프링 컨테이너 생성
2. 스프링 빈 생성
3. 의존 관계 주입
4. 초기화 콜백
5. 사용
6. GC에 의해 수거

### ***싱글톤 빈은 Thread-Safe한가?***

결론부터 말하자면 Thread-Safe하지 않다. 스프링은 싱글톤 레지스트리를 통해 private 생성자, static 변수 등의 코드 없이 비즈니스 로직에 집중하고 테스트 코드에 용이한 싱글톤 객체를 제공해 주는 것 뿐이지, 동기화 문제는 개발자가 처리해야 한다. 만약에 싱글톤 빈이 상태를 갖게 되고, 아무런 동기화 처리를 하지 않는다면 멀티 스레드 환경에서 부작용이 발생할 수 있으니 주의해야 한다.

> 참고해보자
> 

[Spring Bean](https://velog.io/@suhongkim98/Spring-Bean)

[[Spring] Spring Bean 총 정리](https://steady-coding.tistory.com/594)

[[Spring] 스프링 빈(Bean)의 개념과 생성 원리](https://atoz-develop.tistory.com/entry/Spring-%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B9%88Bean%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%83%9D%EC%84%B1-%EC%9B%90%EB%A6%AC)

[[Spring] 스프링 빈을 등록하는 두 가지 방법](https://mimah.tistory.com/entry/Spring-%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B9%88%EC%9D%84-%EB%93%B1%EB%A1%9D%ED%95%98%EB%8A%94-%EB%91%90-%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95)

[[10분 테코톡] 주디의 Spring Bean](https://www.youtube.com/watch?v=3gURJvJw_T4&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=56&ab_channel=%EC%9A%B0%EC%95%84%ED%95%9CTech)

+SSAFY 1017 ppt

[[Spring] 스프링 Bean, IoC Container, DI가 뭔데!!](https://velog.io/@jkijki12/Spring-%EC%8A%A4%ED%94%84%EB%A7%81-Bean-IoC-Container-DI%EA%B0%80-%EB%AD%94%EB%8D%B0)