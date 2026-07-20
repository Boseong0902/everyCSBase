# Spring 면접 질문

## Dispatcher Servlet

관련 개념: [[Dispatcher Servlet]]

- Dispatcher Servlet은 Spring MVC 요청 흐름에서 어떤 역할을 하는가?
- Dispatcher Servlet이 공통 처리 작업을 담당한다는 말은 무엇인가?
- Dispatcher Servlet과 개별 Controller의 책임은 어떻게 나뉘는가?
- Dispatcher Servlet으로 처리하기 어려운 공통 관심사는 어떤 것이 있는가?

## DI와 IoC

관련 개념: [[DI와 IoC]], [[싱글톤]], [[DIP - 의존 관계 역전]]

- DI란 무엇인가?
- IoC란 무엇이고, 기존 객체 생성 방식과 무엇이 다른가?
- 스프링 컨테이너가 의존 객체를 주입하면 어떤 장점이 생기는가?
- Bean이란 무엇인가?
- DI가 강한 결합을 느슨한 결합으로 바꾸는 이유는 무엇인가?

## AOP

관련 개념: [[스프링 AOP]], [[프록시]], [[Annotation]]

- AOP란 무엇인가?
- 핵심 관심사와 공통 관심사를 구분해보라.
- Spring AOP는 왜 프록시 기반으로 동작하는가?
- Advice는 무엇인가?
- `@Transactional`이 AOP로 처리되면 어떤 흐름으로 begin, commit, rollback이 수행되는가?
- Dispatcher Servlet과 AOP는 공통 처리 관점에서 어떻게 다른가?

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
