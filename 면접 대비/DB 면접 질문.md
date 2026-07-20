# DB 면접 질문

## 키와 JOIN

관련 개념: [[키]], [[SQL JOIN]], [[JOIN 성능 한계와 확장 전략]]

- 키란 무엇인가?
- JOIN이란 무엇인가?
- Inner Join과 Outer Join의 차이는 무엇인가?
- Left Outer Join과 Right Outer Join은 기준 테이블이 어떻게 다른가?
- Cross Join과 Full Outer Join의 차이는 무엇인가?
- Self Join은 언제 사용하는가?
- JOIN이 많아질수록 어떤 성능 문제가 생기는가?

## SQL vs NoSQL

관련 개념: [[SQL vs NoSQL]]

- SQL의 장점과 단점은 무엇인가?
- NoSQL의 장점과 단점은 무엇인가?
- SQL은 왜 수평적 확장이 어렵다고 보는가?
- NoSQL은 왜 유연하지만 데이터 중복 문제가 생길 수 있는가?

## 이상 현상과 정규화

관련 개념: [[데이터베이스 이상 현상]], [[정규화와 역정규화]]

- 데이터베이스 이상 현상이란 무엇인가?
- 삽입 이상, 갱신 이상, 삭제 이상을 설명해보라.
- 정규화란 무엇인가?
- 1NF, 2NF, 3NF의 목적은 각각 무엇인가?
- 언제 정규화를 더 해야 하는가?
- 언제 역정규화를 고려해야 하는가?
- 정규화와 JOIN 비용은 어떤 트레이드오프를 가지는가?

## 인덱스

관련 개념: [[인덱스]]

- 인덱스란 무엇인가?
- 인덱스를 언제 고려해야 하는가?
- 클러스터형 인덱스와 비클러스터형 인덱스의 차이는 무엇인가?
- 복합 인덱스란 무엇인가?
- 커버링 인덱스란 무엇인가?
- B-Tree와 B+Tree의 차이는 무엇인가?
- Hash 인덱스는 어떤 조건에서 유리한가?
- 인덱스가 DML 성능을 떨어뜨리는 이유는 무엇인가?
- 카디널리티가 낮은 컬럼에 인덱스를 피해야 하는 이유는 무엇인가?

## 트랜잭션

관련 개념: [[트랜잭션]], [[트랜잭션 격리 수준]]

- 트랜잭션이란 무엇인가?
- ACID를 설명해보라.
- Commit과 Rollback은 무엇인가?
- Savepoint는 언제 사용하는가?
- WAL 원칙이란 무엇인가?
- MySQL InnoDB의 undo log와 redo log는 각각 어떤 역할을 하는가?
- PostgreSQL의 xmin, xmax, CLOG는 무엇인가?
- MVCC는 왜 필요한가?
- 공유락과 배타락의 차이는 무엇인가?

## MySQL과 PostgreSQL

관련 개념: [[MySQL과 PostgreSQL 차이]], [[인덱스]], [[트랜잭션]]

- PostgreSQL 연결이 MySQL보다 비싸다고 보는 이유는 무엇인가?
- PgBouncer는 왜 필요한가?
- PostgreSQL의 트랜잭션 DDL은 어떤 장점이 있는가?
- Materialized View는 일반 View와 어떻게 다른가?
- MySQL은 읽기 작업에서 어떤 장점을 가지는가?
- MySQL의 클러스터링 인덱스는 어떤 장점을 가지는가?
- PostgreSQL의 죽은 튜플은 읽기 성능에 어떤 영향을 줄 수 있는가?

## Redis 캐시

관련 개념: [[Redis 캐시]]

- Redis는 어떤 특성을 가진 데이터베이스인가?
- Cache Hit과 Cache Miss는 무엇인가?
- 캐시와 DB 사이의 데이터 정합성 문제는 왜 생기는가?
- Look Aside와 Read Through의 차이는 무엇인가?
- Write Back, Write Through, Write Around의 차이는 무엇인가?
- Cache Aside + Write Through 조합은 어떤 장단점이 있는가?
- Cache Aside + Write Behind는 어떤 서비스에 적합한가?
- Cache Stampede란 무엇인가?
