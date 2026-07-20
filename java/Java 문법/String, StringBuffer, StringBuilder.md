# String, StringBuffer, StringBuilder

## String

`String`은 불변 객체다.

문자열 내용을 바꾸는 연산이 실행되면 기존 객체의 내용이 바뀌는 것이 아니라, 수정된 내용을 담은 새 객체가 생성된다.

## StringBuffer

`StringBuffer`는 가변 객체이고 thread-safe하다.

내용을 내부 버퍼의 크기를 조절하는 방식 등으로 바꾼다. 모든 주요 메서드에 `synchronized`가 걸려 있어 멀티 스레드 환경에서 안전하게 동작한다.

다만 싱글 스레드 환경에서는 race condition이 없어도 락 획득과 해제 비용이 발생하므로 불필요한 오버헤드가 생긴다.

## StringBuilder

`StringBuilder`는 가변 객체이고 thread-unsafe하다.

`synchronized`를 사용하지 않기 때문에 싱글 스레드 환경에서 문자열을 반복적으로 변경할 때 효율적이다.

## 선택 기준

- 문자열 값이 거의 바뀌지 않으면 `String`
- 멀티 스레드에서 같은 문자열 버퍼를 공유하며 변경해야 하면 `StringBuffer`
- 싱글 스레드에서 문자열을 반복 변경하면 `StringBuilder`

## 관련 개념

- [[Interned String]]
- [[synchronized, volatile 키워드]]
- [[고유락]]
