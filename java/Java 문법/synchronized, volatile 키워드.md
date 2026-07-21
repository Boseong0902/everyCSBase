# synchronized, volatile 키워드

`synchronized`와 `volatile`은 멀티스레드 환경에서 JVM의 메모리 동작과 직접 연결되는 키워드이다.

둘 다 여러 스레드가 공유 데이터에 접근할 때 생길 수 있는 문제를 다루지만, 해결하는 범위가 다르다.

동시성 문제가 왜 생기는지는 [[동시성 문제 - 원자성, 가시성, Race Condition]]에서 먼저 정리한다.

## synchronized

`synchronized`는 한 번에 하나의 스레드만 특정 코드 영역에 들어가게 만든다.

```java
public class Counter {
    private int count;

    public synchronized void increase() {
        count++;
    }
}
```

위 코드에서 여러 스레드가 동시에 `increase()`를 호출해도 한 시점에는 하나의 스레드만 메서드 안으로 들어간다.

## synchronized와 JVM 동작

`synchronized`는 객체의 모니터 락을 사용한다.

인스턴스 메서드에 붙으면 현재 객체의 락을 사용하고, `static synchronized` 메서드에 붙으면 클래스 객체의 락을 사용한다.

```java
public synchronized void instanceMethod() {
}

public static synchronized void staticMethod() {
}
```

- 인스턴스 `synchronized` 메서드: 각 객체 단위로 락이 걸린다
- `static synchronized` 메서드: 클래스 단위로 락이 걸린다

## synchronized가 보장하는 것

`synchronized`는 크게 두 가지를 보장한다.

- 한 번에 하나의 스레드만 임계 영역에 들어가게 한다
- 락을 얻고 해제하는 시점을 기준으로 스레드 간 메모리 가시성을 보장한다

메모리 가시성이란 한 스레드가 변경한 값을 다른 스레드가 볼 수 있게 되는 성질이다.

## volatile

`volatile`은 변수 값을 스레드별 캐시가 아니라 메인 메모리 기준으로 읽고 쓰게 만드는 키워드이다.

```java
public class Flag {
    private volatile boolean running = true;

    public void stop() {
        running = false;
    }

    public void run() {
        while (running) {
            // 작업 수행
        }
    }
}
```

한 스레드가 `running = false`로 바꾸면 다른 스레드가 그 변경을 볼 수 있어야 한다.

이런 플래그 값에는 `volatile`이 자주 사용된다.

## volatile이 보장하는 것

`volatile`은 메모리 가시성을 보장한다.

하지만 복합 연산의 원자성을 보장하지는 않는다.

```java
private volatile int count;

public void increase() {
    count++;
}
```

`count++`는 읽기, 증가, 쓰기가 합쳐진 연산이다.

따라서 `volatile`만으로 여러 스레드가 동시에 증가시키는 상황을 안전하게 만들 수 없다.

이 경우에는 `synchronized`나 원자 클래스가 필요하다.

## 비교

| 키워드            | 핵심 역할                      | 보장하는 것         |
| -------------- | -------------------------- | -------------- |
| `synchronized` | 임계 영역에 락을 건다               | 상호 배제, 메모리 가시성 |
| `volatile`     | 변수 읽기/쓰기를 메모리 가시성 기준으로 다룬다 | 메모리 가시성        |

## 관련 개념

- [[Java 문법]]
- [[Java 동시성]]
- [[동시성 문제 - 원자성, 가시성, Race Condition]]
- [[고유락]]
- [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]
- [[static, final 키워드]]
