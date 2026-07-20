# Record

Record는 DTO나 Entity처럼 값을 전달하는 목적의 객체를 만들 때 반복적으로 작성하던 보일러 플레이트 코드를 줄이기 위한 문법이다.

## 일반 클래스

```java
public class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

## Record

```java
public record Person(String name, int age) {}
```

Record는 필드를 자동으로 `private final`로 선언하고, 생성자와 접근자 메서드를 암묵적으로 생성한다.

## Getter 이름

기존 Java Bean 스타일 getter와 이름이 다르다.

- 일반 클래스: `getName()`
- Record: `name()`

## 관련 개념

- [[Java 문법]]
- [[static, final 키워드]]
- [[불변 객체]]
