# Error와 Exception

Java에서 문제 상황은 모두 `Throwable`을 상속받는 객체로 표현된다.

크게 `Error`와 `Exception`으로 나눈다.

## Error

시스템 레벨의 심각한 문제다.

일반적으로 애플리케이션 코드에서 복구하기 어렵다.

예시는 다음과 같다.

- `OutOfMemoryError`
- `StackOverflowError`

## Exception

프로그램 로직에서 발생하는 예외다.

`try-catch`로 처리할 수 있고, 상황에 따라 복구 가능하다.

예시는 다음과 같다.

- `NullPointerException`
- `IOException`
- `SQLException`

## Checked Exception

컴파일러가 처리를 강제하는 예외다.

주로 서버 외부와 통신하거나 IO를 수행하는 과정에서 발생할 수 있는 예외들이 여기에 해당한다.

- `IOException`
- `SQLException`

## Unchecked Exception

컴파일 시점에 처리를 강제하지 않고 런타임에 발생하는 예외다.

`RuntimeException` 하위 예외들이 여기에 해당한다.

- `NullPointerException`
- `IndexOutOfBoundsException`

## 관련 개념

- [[Java 문법]]
- [[Spring JDBC]]
