# 스프링 AOP

AOP - 핵심 비지니스 로직과 공통 관심사를 분리하는 프로그래밍 방식

Spring AOP - AOP를 스프링에서 [[프록시]] 패턴을 사용하여 구현한 방식

- 즉, 비지니스 로직안에 트랜잭션(커밋, 롤백) 등의 공통 처리 코드를 넣지 않는게 목적이다
- 스프링이 프록시 객체를 만들려면 객체를 컨테이너가 관리해야되기 때문에 Spring Bean에 등록해야 한다

## 핵심 관심사와 공통 관심사

AOP는 애플리케이션을 핵심 관심사와 공통 관심사로 나누어 바라보는 패러다임이다.

- 핵심 관심사: 각 모듈이 실제로 수행해야 하는 고유 비지니스 로직
- 공통 관심사: 여러 모듈에 공통적이고 반복적으로 등장하는 부가 기능

AOP는 공통 관심사를 별도 모듈로 분리하고, 핵심 로직 코드를 직접 수정하지 않고 필요한 지점에 적용한다.

[[Dispatcher Servlet]]도 웹 요청에 대한 공통 처리는 할 수 있지만, 웹 요청이 없는 `@Scheduled` 작업이나 메시지 큐 리스너에는 적용되지 않는다. `@Transactional`처럼 메서드 단위로 작동해야 하는 기능은 Spring AOP가 더 적절하다.

Spring AOP는 런타임에 대상 객체를 감싸는 프록시 객체를 만들고, 메서드 호출을 프록시가 가로채서 Advice를 실행한 뒤 실제 객체를 호출하는 방식으로 동작한다.

Advice는 공통 기능을 언제 적용할지를 정의하는 부분이다.

## 프록시가 만들어지는 대표적인 스프링 패턴

`@Transactional`, `@Cacheable`, `@Async`, `@PreAuthorize`, `@Secured`, `@Retryable`

### 트랜잭션 처리 - @Transactional

```java
@Service
public class OrderService {
    @Transactional
    public void order() {
        orderRepository.save();
        paymentService.pay();
    }
}
```

- 우리가 보기엔 그냥 order()를 호출하는 것 같지만, 실제로는 spring이 만든 프록시를 거친다
	- Controller -> OrderService Proxy -> 트랜잭션 시작 -> 실제 OrderService.order() 호출 -> 성공하면 커밋 -> 예외 발생 시 rollback
- 따라서 개발자가 매번 트랜잭션 성공 시 커밋, 실패 시 rollback 하는 예외 처리 코드를 작성할 필요가 없이, 프록시가 공통으로 처리한다

### 캐싱 - @Cacheable

```java
@Service
public class ProductService {
    @Cacheable("products")
    public Product getProduct(Long id) {
        return productRepository.findById(id);
    }
}
```

- ProductService Proxy -> 캐시에 id가 있는지 확인 -> 있으면 실제 메서드 호출 없이 캐시 반환 -> 없으면 실제 getProduct() 호출 -> 결과를 캐시에 저장 -> 반환

즉, 프록시가 실제 객체 호출 여부를 제어한다

**Q. 그럼 여기서 사용하는 캐시는 로컬캐시? 이거랑 카페인이랑 뭐가 다르지?**

-> 이 어노테이션은 이 데이터를 캐시에 저장해야된다라고 알려주는 기능일 뿐.

-> 어디에 저장할지는 별도의 구현체에 따라 달라진다

이게 JVM 메모리 캐시, redis, caffeine 등등이 될 수 있다

### 권한 검사 - @PreAuthorize

```java
@Service
public class AdminService {
    @PreAuthorize("hasRole('ADMIN')")
    public void deleteUser(Long userId) {
        userRepository.deleteById(userId);
    }
}
```

보안에서도 사용

- AdminService Proxy -> 현재 사용자 권한 확인 -> 권한 없으면 예외 처리 -> 권한 있으면 실제 deleteUser() 호출

### 비동기 처리 - @Async

```java
@Service
public class MailService {
    @Async
    public void sendMail(String email) {
        // 메일 발송
    }
}
```

호출부는 그냥 메서드를 호출함 - `mailService.sendMail("test@test.com");`

여기서 프록시가 중간에서 실제 메서드를 다른 스레드에서 실행하도록 넘긴다

MailService Proxy -> Executor에 작업 제출 -> 호출자는 바로 반환 -> 별도의 스레드에서 실제 sendMail() 실행

**Q. 그럼 @Async 어노테이션이 붙은 작업은 오직 스프링 전역에서 하나의 스레드가 처리하는거야?**

-> ㄴㄴ 스레드 풀이 처리

### 로깅, 성능 측정

직접 AOP를 만들어서 특정 메서드 호출 시간을 측정하기도 함

```java
@Around("execution(* com.example..*Service.*(..))")
public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
    long start = System.currentTimeMillis();

    Object result = joinPoint.proceed();

    long end = System.currentTimeMillis();
    System.out.println("실행 시간: " + (end - start) + "ms");

    return result;
}
```

이러면, 위의 코드, 즉 시간 측정 코드는 비지니스 로직에 들어가지 않는다

**Q. 실제 모니터링 스택 같은걸 사용할 때, 프록시 객체(AOP)를 직접 만들어서 사용해?**

- 일반적인 메트릭이나 로그들은 이미 존재하는 툴들이 잘 수집함
- 따라서 도메인 비지니스 로직 관련된 메트릭(ex> 평균 매칭 대기 시간) 등을 측정하기 위해서 사용

### JPA 지연 로딩

JPA에서도 프록시 개념이 나온다

`Member member = entityManager.getReference(Member.class, 1L);`

위의 경우, DB에서 바로 실제 Member를 가져오지 않고, 프록시 객체를 반환할 수도 있음

Member Proxy -> 처음에는 id만 가지고 있음 -> getName() 같은 실제 필드 접근 시점에 DB조회 -> 실제 데이터 로딩

## 관련 개념

- [[프록시]]
- [[GoF]]
- [[싱글톤]]
- [[Dispatcher Servlet]]
- [[Annotation]]
