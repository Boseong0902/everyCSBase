# SQL JOIN

두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법

두 테이블에서 교차 검색하려면, 결국 같은 단위의 튜플이 있어야 하고, 이 튜플들이 서로 같은 단위, 즉 같은 존재라는 것을 판별할 수 있어야 하므로 두 테이블에서 공유하고있는 속성이 있어야 한다

## Inner Join

교집합

```sql
SELECT A.NAME, B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

A테이블엔 `NO_EMP`, `NAME`이 저장되어있고,

B테이블엔 `NO_EMP`, `AGE`가 저장되어있다면,

`NO_EMP`가 겹치는 사원의 `NAME`과 `AGE`를 가져온다

결국 두 테이블 모두에 `NO_EMP`가 등록되어있어야 한다

## Left Outer Join

왼쪽 테이블을 기준으로 오른쪽 테이블에서 해당하는 정보를 부가적으로 붙이는 join

합집합(합집합 - 여집합)

```sql
SELECT A.NAME, B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

B테이블에 `NO_EMP`가 없는 사원에 대한 `NAME`도 출력된다. 이 경우 `AGE`는 `NULL`이다.

## Right Outer Join

오른쪽 테이블을 기준으로 왼쪽 테이블에서 해당하는 정보를 부가적으로 붙이는 join

## Full Outer Join

합집합

```sql
SELECT A.NAME, B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

## Cross Join

모든 튜플들의 조합

예: `A(1,2,3,4)`, `B(a,b,c,d)`

```sql
SELECT A.number, B.letter
FROM A CROSS JOIN B
```

결과는 `(1, a), (1, b), (1, c), (1, d), (2, a), (2, b) ...`

## Cross Join vs Full Outer Join

Cross Join은 가능한 모든 경우의 수

Full Outer Join은 매칭된 레코드 + 남는 레코드까지 덧붙이는것

## Self Join

자기 자신과의 조인

## 관련 개념

- [[DB]]
- [[JOIN 성능 한계와 확장 전략]]
- [[정규화와 역정규화]]
- [[인덱스]]

