# static, final 키워드

`static`과 `final`은 자바에서 자주 함께 보이지만 의미가 다르다.

- `static`은 객체가 아니라 클래스에 속한다는 의미에 가깝다
- `final`은 한 번 정해진 값을 바꾸지 못하게 하거나, 상속/오버라이딩을 제한한다는 의미에 가깝다

이 문서에서는 특히 JVM 메모리 관점에서 `static`과 `final`이 어떤 차이를 만드는지를 중심으로 본다.

## static

`static`이 붙은 멤버는 인스턴스가 아니라 클래스에 속한다.

객체를 만들지 않아도 클래스 이름으로 접근할 수 있다.

```java
public class Counter {
    static int count = 0;

    public Counter() {
        count++;
    }
}
```

```java
Counter a = new Counter();
Counter b = new Counter();

System.out.println(Counter.count); // 2
```

`count`는 각 객체가 따로 가지는 값이 아니라 `Counter` 클래스가 공유하는 값이다.

## static과 메모리

`static` 변수는 클래스가 로딩될 때 클래스 정보와 함께 메서드 영역 쪽에서 관리된다.[[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]

반면 인스턴스 필드는 객체가 생성될 때 힙 영역의 객체 내부에 생긴다.

```java
public class User {
    static int userCount;
    String name;
}
```

- `userCount`는 `User` 클래스에 속한다
- `name`은 `new User()`로 만들어진 각 객체에 속한다

## static 메서드

`static` 메서드는 객체 없이 호출할 수 있다.

```java
public class MathUtil {
    public static int add(int a, int b) {
        return a + b;
    }
}
```

```java
int result = MathUtil.add(1, 2);
```

단, `static` 메서드는 특정 객체에 속한 메서드가 아니기 때문에 인스턴스 필드에 직접 접근할 수 없다.

```java
public class User {
    private String name;

    public static void printName() {
        // System.out.println(name); // 불가능
    }
}
```

## final

`final`은 더 이상 바꿀 수 없게 만든다는 의미이다.

어디에 붙는지에 따라 제한 대상이 달라진다.

## final 변수

`final` 변수는 한 번 초기화하면 다시 값을 대입할 수 없다.

```java
final int value = 10;
// value = 20; // 불가능
```

참조형 변수에 `final`을 붙이면 참조값을 다시 바꿀 수 없다.

객체 내부 상태까지 항상 불변이 되는 것은 아니다.

```java
final List<String> names = new ArrayList<>();
names.add("kim"); // 가능
// names = new ArrayList<>(); // 불가능
```

## final 필드와 메모리

`final` 인스턴스 필드는 객체가 생성될 때 값이 정해지고, 그 객체 안에서 다시 대입할 수 없다.

즉, 필드 자체는 힙 영역의 객체 내부에 있고, `final`은 그 필드에 대한 재대입을 막는다.

```java
public class Person {
    private final String name;

    public Person(String name) {
        this.name = name;
    }
}
```

`name`은 각 `Person` 객체마다 따로 존재한다.

`final`은 저장되는 메모리 영역 자체를 바꾸지는 않는다.

지역 변수에 붙으면 스택 프레임 안의 지역 변수 재대입을 막고, 인스턴스 필드에 붙으면 힙 영역 객체 내부 필드의 재대입을 막고, `static final`에 붙으면 클래스 단위 상수처럼 사용된다.

## static final

`static final`은 클래스 단위로 하나만 존재하면서, 값도 바뀌지 않는 상수를 만들 때 자주 사용한다.

```java
public class AppConfig {
    public static final int MAX_RETRY_COUNT = 3;
}
```

이 값은 특정 객체가 아니라 `AppConfig` 클래스에 속한다.

그래서 여러 객체가 공유해도 값이 바뀌지 않는 설정값이나 상수에 적합하다.

## final 메서드

`final` 메서드는 자식 클래스에서 오버라이딩할 수 없다.

```java
public class Parent {
    public final void run() {
        System.out.println("run");
    }
}
```

부모 클래스에서 정한 메서드의 동작을 자식 클래스가 바꾸지 못하게 하고 싶을 때 사용한다.

## final 클래스

`final` 클래스는 상속할 수 없다.

```java
public final class StringUtil {
}
```

클래스의 확장을 막고, 설계한 형태 그대로만 사용하게 만들고 싶을 때 사용한다.

## static과 final 비교

| 키워드 | 핵심 의미 | 메모리 관점 |
| --- | --- | --- |
| `static` | 클래스에 속한다 | 클래스 로딩 시 클래스 단위로 관리된다 |
| `final` | 다시 바꿀 수 없게 한다 | 저장 위치를 바꾸는 키워드가 아니라 재대입/상속/오버라이딩을 제한한다 |
| `static final` | 클래스 단위 상수 | 클래스에 속하며 값 변경이 제한된다 |

## 관련 개념

- [[Java]]
- [[Java 문법]]
- [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]
- [[객체지향 프로그래밍의 개념 이해]]
- [[LSP - 리스코프 치환]]
- [[synchronized, volatile 키워드]]
