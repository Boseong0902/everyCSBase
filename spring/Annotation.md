# Annotation

Annotation은 클래스, 필드, 메서드, 파라미터 등에 메타데이터를 부여하는 방식이다.

컴파일러나 프레임워크가 어노테이션을 읽고 특정 기능을 수행할 수 있다.

## 예시

- `@Override`: 메서드 오버라이딩 여부를 컴파일러가 확인한다.
- `@Transactional`: 트랜잭션 경계를 선언한다.
- `@Autowired`: 타입 기준으로 의존성을 자동 주입한다.
- `@GetMapping`, `@PostMapping`: 특정 메서드를 요청 URL과 매핑한다.
- `@RequestParam`, `@RequestBody`: 요청 파라미터나 본문을 메서드 인자로 바인딩한다.

## 스프링에서의 역할

스프링은 어노테이션을 통해 Bean 등록, 의존성 주입, 요청 매핑, 트랜잭션 처리 같은 기능을 선언적으로 적용한다.

## 관련 개념

- [[DI와 IoC]]
- [[Dispatcher Servlet]]
- [[스프링 AOP]]
- [[오버라이딩 vs 오버로딩]]
