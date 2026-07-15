# Java 문법과 JVM 면접 질문

## JVM 메모리 영역

관련 개념: [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]

- JVM 런타임 메모리 영역을 설명해보라.
- 메서드 영역에는 무엇이 저장되는가?
- 스택 영역에는 무엇이 저장되는가?
- 힙 영역에는 무엇이 저장되는가?
- 기본형 지역 변수와 참조형 지역 변수는 메모리에서 어떻게 다르게 저장되는가?
- 객체와 배열은 어디에 저장되는가?

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
- synchronized와 volatile의 차이는 무엇인가?

## transient

관련 개념: [[transient 키워드]]

- transient 키워드는 언제 사용하는가?
- transient 필드는 힙 영역에 존재하지 않는가?
- transient 필드는 직렬화와 역직렬화 과정에서 어떻게 처리되는가?

