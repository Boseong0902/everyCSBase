# Garbage Collection

Java의 모든 객체는 힙 메모리에 저장된다.

C/C++은 `malloc/free`, `new/delete`로 개발자가 직접 메모리 할당과 해제를 관리하지만, Java는 JVM의 GC가 참조 여부를 기준으로 메모리를 관리한다.

## 기본 동작

GC는 GC Root에서 시작해 참조 체인을 따라가며 살아 있는 객체를 찾는다.

- Mark: GC Root에서 도달 가능한 객체를 표시한다.
- Sweep: 표시되지 않은 객체를 메모리에서 제거한다.
- Compact: 살아남은 객체를 한쪽으로 모아 메모리 단편화를 줄인다.

GC Root에는 스택의 지역 변수, static 필드 등이 포함된다.

## Young Generation과 Old Generation

전체 힙을 매번 검사하면 비용이 크기 때문에, JVM은 객체 생명주기 특성을 이용해 힙을 세대별로 나누어 관리한다.

대부분의 객체는 생성 직후 금방 사라지고, 오래 살아남은 객체는 계속 살아남는 경향이 있다.

Young Generation은 다시 Eden, Survivor S0, Survivor S1으로 나뉜다.

1. 새 객체는 Eden 영역에 할당된다.
2. Eden이 가득 차면 Minor GC가 발생한다.
3. Eden에서 살아남은 객체는 Survivor 영역으로 이동한다.
4. 이후 Minor GC마다 살아남은 객체는 S0과 S1 사이를 이동하며 age가 증가한다.
5. age가 임계값에 도달하면 Old Generation으로 승격된다.

## Minor GC와 Major GC

| 구분 | Minor GC | Major GC |
| --- | --- | --- |
| 대상 | Young Generation | Old Generation |
| 빈도 | 자주 발생 | 드물게 발생 |
| 속도 | 빠름 | 느림 |
| STW | 짧음 | 김 |

## Stop The World

GC가 실행되면 GC 스레드를 제외한 애플리케이션 스레드가 멈출 수 있다.

GC가 Mark를 수행하는 동안 다른 스레드가 참조 관계를 바꾸면, 지워야 할 대상을 살리거나 살려야 할 대상을 지울 수 있다. 그래서 GC 튜닝의 핵심은 STW 시간을 줄이는 것이다.

## PermGen에서 MetaSpace로

기존 JVM의 PermGen에는 클래스 메타데이터, 메서드 바이트코드, 런타임 상수 풀, `static` 변수 등이 저장되었다.

하지만 Spring처럼 [[스프링 AOP|프록시 클래스]]를 동적으로 많이 생성하는 환경에서는 고정 크기의 PermGen이 가득 차 OOM이 발생하기 쉬웠다. 이후 MetaSpace로 대체되면서 힙 외부의 OS 네이티브 메모리를 사용하고, 동적으로 확장할 수 있게 되었다.

## GC 알고리즘

### Serial GC

싱글 스레드로 GC를 수행한다.

### Parallel GC

멀티 스레드로 GC를 수행해 처리량을 높인다.

마킹 단계에서는 여러 스레드가 어떤 객체를 마킹할지 결정하므로 race condition이 생길 수 있고, CAS 같은 원자적 연산으로 해결한다.

### G1 GC

힙을 고정된 Young/Old 영역으로만 나누지 않고 Region 단위로 쪼개서 관리한다.

가비지가 많은 Region부터 수거하며, 각 Region의 역할은 Eden, Survivor, Old, Humongous, Free 등으로 동적으로 바뀔 수 있다.

### ZGC

STW 시간을 매우 짧게 줄이는 것을 목표로 하는 GC다.

## 관련 개념

- [[JVM]]
- [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]
- [[스프링 AOP]]
- [[synchronized, volatile 키워드]]
