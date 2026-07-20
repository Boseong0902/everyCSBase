# Spring JDBC

Spring JDBC는 전통적인 JDBC 사용 시 반복적으로 처리해야 하는 작업을 줄여준다.

순수 JDBC에서는 매번 다음 과정을 직접 처리해야 한다.

- 커넥션 획득
- 쿼리 생성과 실행
- 결과 매핑
- 예외 처리
- 자원 해제

Spring JDBC를 사용하면 개발자는 SQL과 매핑 로직에 더 집중할 수 있다.

## 자동으로 처리하는 것

- 커넥션 획득과 반환
- 파라미터 바인딩
- 예외 변환
- 자원 해제

## 예외 변환

JDBC의 `SQLException`은 DB마다 에러 코드가 제각각이다.

스프링은 이를 `DataAccessException`이라는 일관된 런타임 예외로 추상화한다. 그래서 특정 DB에 강하게 묶인 예외 처리 대신 일관된 예외 처리를 할 수 있다.

## 더 높은 추상화

더 고수준의 데이터베이스 접근 추상화가 필요하면 JPA, Hibernate 같은 ORM을 사용할 수 있다.

## 관련 개념

- [[DAO와 Repository]]
- [[Error와 Exception]]
- [[트랜잭션]]
- [[SQL vs NoSQL]]
