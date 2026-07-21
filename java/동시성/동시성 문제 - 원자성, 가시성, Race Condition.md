# 동시성 문제 - 원자성, 가시성, Race Condition

여러 스레드가 같은 데이터를 공유하면 실행 순서와 메모리 반영 시점에 따라 예상과 다른 결과가 나올 수 있다.

동시성 문제는 크게 race condition, 원자성, 메모리 가시성으로 나누어 보면 이해하기 쉽다.

## Race Condition

Race condition은 여러 스레드가 같은 데이터를 동시에 읽고 쓰면서, 실행 순서에 따라 결과가 달라지는 문제다.

```java
class Counter {
    private int count;

    void increase() {
        count++;
    }
}
```

`count++`는 한 줄처럼 보이지만 실제로는 다음 단계로 나뉜다.

1. 현재 `count` 값을 읽는다.
2. 값을 1 증가시킨다.
3. 증가한 값을 다시 저장한다.

두 스레드가 동시에 같은 값을 읽으면, 둘 다 증가시켜 저장하더라도 한 번의 증가가 사라질 수 있다.

## 원자성

원자성은 작업이 중간에 끊기지 않고 하나의 단위처럼 실행되는 성질이다.

`count++`는 읽기, 증가, 쓰기가 합쳐진 복합 연산이므로 원자적이지 않다.

이런 작업은 [[synchronized, volatile 키워드|synchronized]]나 원자 클래스 같은 도구로 보호해야 한다.

## 메모리 가시성

메모리 가시성은 한 스레드가 바꾼 값을 다른 스레드가 볼 수 있는 성질이다.

스레드는 성능을 위해 값을 CPU 캐시나 작업 메모리에 들고 있을 수 있다. 그래서 어떤 스레드가 값을 바꿨더라도 다른 스레드가 즉시 그 변경을 본다고 단정할 수 없다.

```java
class Runner {
    private boolean running = true;

    void stop() {
        running = false;
    }

    void run() {
        while (running) {
            // 작업
        }
    }
}
```

한 스레드가 `stop()`을 호출해도, 다른 스레드가 `running` 변경을 보지 못하면 반복문이 끝나지 않을 수 있다.

이런 단순 상태 플래그의 변경 전파에는 [[synchronized, volatile 키워드|volatile]]을 사용할 수 있다.

## 해결 방향

| 문제 | 대표 해결책 |
| --- | --- |
| 동시에 같은 값을 수정해서 결과가 꼬임 | `synchronized`, 원자 클래스 |
| 한 스레드의 변경을 다른 스레드가 못 봄 | `volatile`, `synchronized` |
| 공유 상태 자체가 너무 많음 | [[불변 객체]], 지역 변수, 스레드별 독립 데이터 |

## 관련 개념

- [[Java 동시성]]
- [[synchronized, volatile 키워드]]
- [[고유락]]
- [[불변 객체]]
