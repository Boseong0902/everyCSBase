# Spring 면접 질문

관련 개념: [[Spring]]

## Dispatcher Servlet

관련 개념: [[Dispatcher Servlet]]

- Dispatcher Servlet은 Spring MVC 요청 흐름에서 어떤 역할을 하는가?
- Dispatcher Servlet이 공통 처리 작업을 담당한다는 말은 무엇인가?
- Dispatcher Servlet과 개별 Controller의 책임은 어떻게 나뉘는가?
- Dispatcher Servlet으로 처리하기 어려운 공통 관심사는 어떤 것이 있는가?
- Dispatcher Servlet은 어떤 방식으로 요청에 맞는 컨트롤러를 찾는가?
- Filter, Interceptor, AOP는 공통 관심사 처리에서 각각 어떻게 다른가?

## DI와 IoC

관련 개념: [[DI와 IoC]], [[싱글톤]], [[DIP - 의존 관계 역전]]

- DI란 무엇인가?
- IoC란 무엇이고, 기존 객체 생성 방식과 무엇이 다른가?
- 스프링 컨테이너가 의존 객체를 주입하면 어떤 장점이 생기는가?
- Bean이란 무엇인가?
- DI가 강한 결합을 느슨한 결합으로 바꾸는 이유는 무엇인가?
- 생성자 주입을 필드 주입보다 선호하는 이유는 무엇인가?
- 스프링 빈의 기본 스코프는 무엇이고, 싱글톤 빈에 상태를 두면 왜 위험한가?
- 같은 타입의 빈이 여러 개일 때 스프링은 무엇을 기준으로 주입 대상을 고르는가?

## AOP

관련 개념: [[스프링 AOP]], [[프록시]], [[Annotation]]

- AOP란 무엇인가?
- 핵심 관심사와 공통 관심사를 구분해보라.
- Spring AOP는 왜 프록시 기반으로 동작하는가?
- Advice는 무엇인가?
- `@Transactional`이 AOP로 처리되면 어떤 흐름으로 begin, commit, rollback이 수행되는가?
- Dispatcher Servlet과 AOP는 공통 처리 관점에서 어떻게 다른가?
- 프록시가 만들어지려면 왜 대상 객체가 빈으로 등록되어 있어야 하는가?
- 같은 클래스 안에서 메서드를 내부 호출하면 AOP가 왜 적용되지 않는가?
- Spring AOP는 JDK 동적 프록시와 CGLIB 중 무엇을 언제 사용하는가?
- Advice, Pointcut, JoinPoint는 각각 무엇인가?
- 프록시가 만들어지는 스프링 어노테이션에는 어떤 것들이 있는가?
- `@Cacheable` 프록시가 실제 메서드 호출 자체를 건너뛸 수 있다는 점은 `@Transactional` 프록시와 무엇이 다른가?
- `@Cacheable`이 실제로 데이터를 어디에 저장할지는 무엇이 결정하는가?
- `@Async`가 붙은 작업은 어떤 스레드가 처리하는가?
- `@Async` 메서드에서 발생한 예외는 왜 호출자에게 전파되지 않는가?
- `@PreAuthorize` 같은 권한 검사도 AOP로 처리하는 이유는 무엇인가?
- JPA 지연 로딩은 프록시와 어떻게 연결되는가?
- 직접 AOP를 만들어 메트릭을 측정하는 것은 어떤 경우에 의미가 있는가?

## 트랜잭션과 이벤트

관련 개념: [[이벤트 리스너와 트랜잭션]], [[분산 트랜잭션]], [[옵저버]]

- `@Transactional`의 전파 속성(REQUIRED, REQUIRES_NEW 등)은 무엇을 제어하는가?
- `@Transactional`은 기본적으로 어떤 예외에서 롤백되는가?
- Checked Exception이 기본 롤백 대상이 아닌 이유는 무엇인가?
- `@EventListener`를 트랜잭션 안에서 사용하면 어떤 문제가 생기는가?
- `@TransactionalEventListener`는 이 문제를 어떻게 해결하는가?
- TransactionPhase 네 가지는 각각 언제 사용하는가?
- `@TransactionalEventListener`를 써도 후속 작업 실패가 롤백으로 이어지지 않는 이유는 무엇인가?
- 후속 작업을 비동기로 바꾸면 어떤 문제가 추가로 생기는가?

## DAO와 Repository

관련 개념: [[DAO와 Repository]], [[Spring JDBC]]

- DAO는 어떤 책임을 갖는 객체인가?
- DAO를 두면 비지니스 로직과 DB 접근 코드가 어떻게 분리되는가?
- DAO와 Repository는 어떻게 구분할 수 있는가?
- JDBC를 사용할 때 DAO라는 이름이 자주 쓰이고, JPA를 사용할 때 Repository라는 이름이 자주 쓰이는 이유는 무엇인가?

## Annotation

관련 개념: [[Annotation]]

- Annotation은 무엇인가?
- Spring에서 Annotation은 어떤 방식으로 사용되는가?
- `@Autowired`는 무엇을 기준으로 의존성을 주입하는가?
- `@GetMapping`, `@PostMapping`은 어떤 역할을 하는가?
- `@RequestParam`과 `@RequestBody`는 어떤 데이터를 바인딩하는가?

## Spring JDBC

관련 개념: [[Spring JDBC]], [[DAO와 Repository]], [[Error와 Exception]]

- 순수 JDBC를 사용할 때 개발자가 반복적으로 처리해야 하는 작업은 무엇인가?
- Spring JDBC는 어떤 작업을 자동화하는가?
- Spring JDBC의 예외 변환은 왜 필요한가?
- `SQLException`을 `DataAccessException`으로 추상화하면 어떤 장점이 있는가?
- Spring JDBC보다 더 높은 수준의 데이터 접근 추상화가 필요하면 무엇을 사용할 수 있는가?
- `DataAccessException`이 체크 예외가 아니라 런타임 예외인 이유는 무엇인가?
- `JdbcTemplate`은 어떤 디자인 패턴으로 구현되어 있는가?
