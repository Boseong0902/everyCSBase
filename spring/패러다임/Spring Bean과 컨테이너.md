# Spring Bean과 컨테이너

Bean은 스프링 컨테이너가 생성하고 관리하는 객체다.

일반 객체는 개발자가 직접 `new`로 만들고 의존 객체도 직접 연결한다. 반면 Bean은 스프링 컨테이너가 생성, 의존성 주입, 생명주기 관리를 담당한다.

## 컨테이너가 하는 일

- Bean 생성
- Bean 간 의존성 연결
- Bean 생명주기 관리
- 설정 정보와 어노테이션 해석
- 필요한 곳에 Bean 주입

## Bean 등록

스프링은 여러 방식으로 Bean을 등록할 수 있다.

```java
@Component
class EmailSender {
}
```

```java
@Service
class OrderService {
}
```

```java
@Configuration
class AppConfig {
    @Bean
    EmailSender emailSender() {
        return new EmailSender();
    }
}
```

`@Component`, `@Service`, `@Repository`, `@Controller` 같은 어노테이션은 클래스를 스프링이 관리할 Bean으로 등록하는 데 사용된다.

`@Bean`은 메서드 반환 객체를 Bean으로 등록한다.

## 기본 스코프

스프링 Bean의 기본 스코프는 싱글톤이다.

즉, 컨테이너 안에서 Bean 객체가 하나만 만들어지고 여러 곳에서 공유된다. 그래서 싱글톤 Bean에 요청별 상태를 필드로 두면 여러 요청이나 스레드가 같은 값을 공유하게 되어 문제가 생길 수 있다.

## DI와의 관계

Bean으로 등록된 객체들은 [[DI와 IoC]]를 통해 서로 연결된다.

```java
@Service
class OrderService {
    private final EmailSender emailSender;

    OrderService(EmailSender emailSender) {
        this.emailSender = emailSender;
    }
}
```

`OrderService`는 `new EmailSender()`를 직접 하지 않는다. 생성자에 필요한 의존성을 선언해두면, 컨테이너가 알맞은 Bean을 찾아 주입한다.

## 관련 개념

- [[Spring 패러다임]]
- [[DI와 IoC]]
- [[Annotation]]
- [[싱글톤]]
- [[정적 팩토리 메서드와 팩토리 메서드]]
