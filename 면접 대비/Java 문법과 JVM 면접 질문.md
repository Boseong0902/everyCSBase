# Java 문법과 JVM 면접 질문

## 자바 컴파일과 JVM 실행 흐름

관련 개념: [[자바 컴파일 과정]], [[JVM]], [[클래스 로더]]

- Java가 OS 독립적으로 실행될 수 있는 이유는 무엇인가?
- `.java` 파일이 실행되기까지 어떤 과정을 거치는가?
- 바이트코드는 무엇이고 JVM은 이를 어떻게 실행하는가?
- 인터프리터와 JIT 컴파일러의 차이는 무엇인가?
- JIT 컴파일러는 어떤 문제를 해결하기 위해 사용되는가?
- 클래스 로더는 어떤 역할을 하는가?
- 클래스 로딩은 어떤 단계를 거쳐 이루어지는가?
- 클래스 로더의 부모 위임 모델은 무엇이며 왜 필요한가?
- 클래스가 프로그램 시작 시점에 전부 로딩되지 않고 동적으로 로딩되는 이유는 무엇인가?
- JIT 컴파일은 왜 별도 스레드에서 비동기적으로 수행되는가?

## JVM 메모리 영역

관련 개념: [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]], [[JVM]]

- JVM 런타임 메모리 영역을 설명해보라.
- 메서드 영역에는 무엇이 저장되는가?
- 스택 영역에는 무엇이 저장되는가?
- 힙 영역에는 무엇이 저장되는가?
- 기본형 지역 변수와 참조형 지역 변수는 메모리에서 어떻게 다르게 저장되는가?
- 객체와 배열은 어디에 저장되는가?
- PC Register와 Native Method Stack은 왜 스레드별로 독립적인가?

## Garbage Collection

관련 개념: [[Garbage Collection]], [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]

- Java에서 GC가 필요한 이유는 무엇인가?
- GC Root에는 어떤 것들이 포함되는가?
- static 변수가 GC Root에 포함되는 이유는 무엇인가?
- GC가 있는 Java에서도 메모리 누수가 발생할 수 있는 이유는 무엇인가?
- Mark, Sweep, Compact 과정을 설명해보라.
- Young Generation과 Old Generation으로 힙을 나누는 이유는 무엇인가?
- Minor GC와 Major GC의 차이는 무엇인가?
- Stop The World는 무엇이고 왜 발생하는가?
- PermGen이 MetaSpace로 바뀐 이유는 무엇인가?
- G1 GC는 기존 GC와 어떤 점이 다른가?
- ZGC는 어떤 문제를 줄이기 위한 GC인가?
- Eden, Survivor S0, S1은 각각 어떤 역할을 하는가?
- 객체가 Old Generation으로 승격되는 기준은 무엇인가?
- Serial GC와 Parallel GC의 차이는 무엇인가?
- Parallel GC의 마킹 단계에서 race condition은 어떻게 해결하는가?
- G1 GC에서 Region의 역할이 동적으로 바뀐다는 말은 무슨 뜻인가?
- 스프링처럼 프록시 클래스를 동적으로 많이 만드는 환경에서 PermGen이 특히 문제가 됐던 이유는 무엇인가?

## static

관련 개념: [[static, final 키워드]], [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]

- static 키워드는 무엇을 의미하는가?
- static 변수는 JVM 메모리 영역 중 어디에서 관리되는가?
- static 메서드는 왜 객체 없이 호출할 수 있는가?
- static 메서드에서 인스턴스 필드에 직접 접근할 수 없는 이유는 무엇인가?
- static 메서드는 왜 오버라이딩할 수 없는가?
- main 메서드는 왜 오버라이딩할 수 없는가?

## final

관련 개념: [[static, final 키워드]], [[LSP - 리스코프 치환]], [[오버라이딩 vs 오버로딩]]

- final 변수는 무엇을 제한하는가?
- final 참조 변수와 객체 불변성은 같은 개념인가?
- final 인스턴스 필드는 메모리 어디에 존재하는가?
- final 메서드는 왜 오버라이딩할 수 없는가?
- final 클래스는 무엇을 제한하는가?
- static final은 어떤 상황에서 사용하는가?

## synchronized와 volatile

관련 개념: [[synchronized, volatile 키워드]]

- synchronized는 무엇을 보장하는가?
- synchronized는 JVM에서 어떤 락을 사용하는가?
- 인스턴스 synchronized와 static synchronized의 차이는 무엇인가?
- volatile은 무엇을 보장하는가?
- volatile만으로 count++ 같은 연산을 안전하게 만들 수 없는 이유는 무엇인가?
- count++를 안전하게 만들려면 synchronized 외에 어떤 방법이 있는가?
- synchronized와 volatile의 차이는 무엇인가?

## transient

관련 개념: [[transient 키워드]]

- transient 키워드는 언제 사용하는가?
- transient 필드는 힙 영역에 존재하지 않는가?
- transient 필드는 직렬화와 역직렬화 과정에서 어떻게 처리되는가?

## Call by Value

관련 개념: [[Call by Value]], [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]

- Java는 Call by Value인가, Call by Reference인가?
- 참조 타입을 메서드 인자로 넘길 때 실제로 무엇이 복사되는가?
- 메서드 안에서 객체 상태 변경은 가능한데 참조 변수 재할당은 호출자에게 반영되지 않는 이유는 무엇인가?
- Java가 포인터 연산을 제거한 것이 캡슐화와 어떻게 연결되는가?

## 문자열

관련 개념: [[String, StringBuffer, StringBuilder]], [[Interned String]], [[불변 객체]]

- String이 불변 객체라는 말은 무엇인가?
- StringBuffer와 StringBuilder의 차이는 무엇인가?
- StringBuffer가 싱글 스레드 환경에서 불필요한 오버헤드를 가질 수 있는 이유는 무엇인가?
- 문자열 리터럴과 `new String()`은 메모리 관점에서 어떻게 다른가?
- `equals()`와 `==`의 차이는 무엇인가?
- String Constant Pool은 어떤 역할을 하는가?
- `intern()`은 어떤 동작을 하는가?
- `String.valueOf()`는 내부적으로 어떻게 동작하는가?
- `String`이 불변이기 때문에 얻는 동시성 측면의 이점은 무엇인가?
- 불변 객체를 만들려면 어떤 조건을 지켜야 하는가?
- String Constant Pool은 JVM 메모리 영역 중 어디에 위치하는가?

## 캐스팅과 다형성

관련 개념: [[캐스팅]], [[정적 다형성과 런타임 다형성]], [[오버라이딩 vs 오버로딩]]

- 업캐스팅과 다운캐스팅을 설명해보라.
- 다운캐스팅이 가능한 조건은 무엇인가?
- 다운캐스팅이 실패하면 어떤 예외가 발생하며 이를 어떻게 방지하는가?
- `instanceof`와 다운캐스팅을 많이 쓰는 코드가 확장성에 불리한 이유는 무엇인가?
- 다운캐스팅 대신 다형성과 오버라이딩으로 해결하는 방식은 무엇인가?

## 직렬화

관련 개념: [[직렬화]], [[transient 키워드]]

- 직렬화란 무엇인가?
- 객체를 JVM 내부 참조 구조 그대로 외부로 보낼 수 없는 이유는 무엇인가?
- Java 네이티브 직렬화의 보안 문제는 무엇인가?
- JSON 직렬화가 실무에서 자주 쓰이는 이유는 무엇인가?
- `ObjectInputFilter`는 어떤 문제를 줄이기 위해 사용하는가?
- `serialVersionUID`는 무엇이며 왜 명시적으로 선언하는가?
- 직렬화는 실무에서 어떤 상황에 사용되는가?

## Error와 Exception

관련 개념: [[Error와 Exception]]

- Error와 Exception의 차이는 무엇인가?
- Checked Exception과 Unchecked Exception의 차이는 무엇인가?
- Java에서 예외와 에러가 모두 객체로 다뤄진다는 말은 무슨 의미인가?
- `RuntimeException` 하위 예외는 왜 컴파일러가 처리를 강제하지 않는가?

## Stream, Record, Collection

관련 개념: [[Java Stream]], [[Record]], [[컬렉션 프레임워크]]

- Stream과 Collection의 차이는 무엇인가?
- Stream의 내부 반복과 Collection의 외부 반복은 어떻게 다른가?
- Stream의 중간 연산과 최종 연산은 어떻게 다르며 지연 연산이란 무엇인가?
- Record는 어떤 보일러 플레이트를 줄여주는가?
- Record의 접근자 메서드 이름은 일반 getter와 어떻게 다른가?
- Record가 자동 생성하는 메서드에는 접근자 외에 무엇이 있는가?
- Record는 상속할 수 있는가?
- List, Set, Queue, Map의 차이를 설명해보라.
- HashSet과 HashMap은 유니크 여부를 어떻게 판단하는가?
- `equals()`와 `hashCode()`를 함께 오버라이딩해야 하는 이유는 무엇인가?
- ArrayList와 LinkedList의 차이는 무엇인가?
- HashMap은 해시 충돌을 어떻게 처리하는가?
- Java 8 이후 HashMap이 버킷을 트리로 바꾸는 이유는 무엇인가?
- `Map`이 `Collection`을 직접 구현하지 않는 이유는 무엇인가?
- HashSet, LinkedHashSet, TreeSet은 순서 측면에서 어떻게 다른가?
- TreeSet과 TreeMap의 정렬 기준은 무엇으로 정하는가?
- `Comparable`과 `Comparator`가 함께 있으면 무엇이 우선되는가?
- `ConcurrentHashMap`은 어떤 방식으로 락 경합을 줄이는가?
- `Map`으로 조회 비용을 줄이는 것이 N+1 문제 완화와 어떻게 연결되는가?
- Stream의 병렬 처리는 어떤 상황에서 오히려 불리한가?

## 스레드와 락

관련 개념: [[스레드 활용 - 멀티 스레딩]], [[고유락]], [[synchronized, volatile 키워드]]

- `Runnable` 구현과 `Thread` 상속 중 어떤 방식을 선호하는가?
- `run()`과 `start()`의 차이는 무엇인가?
- Java 스레드의 주요 상태를 설명해보라.
- `wait()`와 `notify()`는 어떤 상황에서 사용하는가?
- Java 객체의 고유락은 무엇인가?
- 재진입 락이란 무엇인가?
- 구조적 락과 명시적 락의 차이는 무엇인가?
- BLOCKED 상태와 WAITING 상태는 무엇이 다른가?
- 명시적 락이 조건별 대기 큐를 분리할 수 있다는 것은 어떤 상황에서 유리한가?
- 생산자-소비자 구조에서 `wait()` 없이 처리하면 어떤 비효율이 생기는가?
- 락이 호출 단위가 아니라 스레드 단위로 소유된다는 말은 무슨 뜻인가?
- 데드락은 어떤 조건에서 발생하며 어떻게 예방하는가?
- 스레드 풀을 사용하는 이유는 무엇인가?
