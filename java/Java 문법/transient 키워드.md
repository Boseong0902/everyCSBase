# transient 키워드

`transient`는 직렬화 대상에서 특정 필드를 제외할 때 사용하는 키워드이다.

객체가 힙 영역에 존재할 때는 필드가 정상적으로 존재하지만, 객체를 바이트 형태로 직렬화할 때 `transient` 필드는 저장 대상에서 빠진다.

```java
public class User implements Serializable {
    private String name;
    private transient String password;
}
```

위 코드에서 `name`은 직렬화되지만, `password`는 직렬화되지 않는다.

## JVM 동작 관점

`transient`는 객체가 메모리에 올라가는 위치를 바꾸지는 않는다.

`transient` 필드도 객체의 인스턴스 필드이므로 힙 영역의 객체 내부에 존재한다.

다만 직렬화 과정에서 해당 필드를 저장하지 않도록 JVM 직렬화 메커니즘에 표시하는 역할을 한다.

## 역직렬화 후 값

직렬화에서 제외된 필드는 역직렬화 후 기본값을 가진다.

```java
// String password -> null
// int value -> 0
// boolean enabled -> false
```

## 사용할 때

- 비밀번호처럼 저장되면 안 되는 값
- 다시 계산할 수 있는 캐시 값
- 직렬화할 필요가 없는 런타임 전용 값

## 관련 개념

- [[Java 문법]]
- [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]
