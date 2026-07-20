# DAO와 Repository

DAO는 데이터베이스에 접근해 CRUD 같은 영속성 로직을 전담하는 객체다.

비지니스 로직을 SQL이나 JDBC 코드와 분리하고, DB 접근을 캡슐화하기 위해 사용한다.

## DAO

DAO는 데이터 저장소 접근에 초점을 둔 개념이다.

JDBC 코드를 직접 다룰 때는 DAO 계층이라는 이름을 쓰는 경우가 많다.

## Repository

Repository는 도메인 객체 컬렉션을 다루는 더 추상화된 개념이다.

JPA를 사용할 때는 Repository 계층이라는 이름을 쓰는 경우가 많다.

## 구분

둘을 엄격하게 구분하지 않고 섞어 쓰기도 한다.

핵심 차이는 DAO가 저장소 접근 구현에 더 가깝고, Repository는 도메인 관점의 컬렉션 추상화에 더 가깝다는 점이다.

## 관련 개념

- [[Spring JDBC]]
- [[SQL vs NoSQL]]
- [[트랜잭션]]
