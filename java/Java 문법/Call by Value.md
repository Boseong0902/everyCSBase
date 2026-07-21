# Call by Value

Java는 항상 Call by Value다.

참조 타입을 인자로 넘길 때도 객체 자체를 넘기는 것이 아니라, 객체를 가리키는 참조값을 복사해서 넘긴다.

## 참조 타입도 Call by Value인 이유

참조 타입 변수에는 객체의 실제 값이 아니라 객체가 있는 위치를 가리키는 참조값이 들어 있다.

메서드 호출 시 이 참조값이 복사되어 전달된다. 그래서 메서드 안에서 참조값을 통해 객체의 내부 상태를 바꿀 수는 있지만, 매개변수 자체를 다른 객체로 바꿔도 호출한 쪽의 참조 변수는 바뀌지 않는다.

## 기본형 예시

```java
public class CallByValueExample {
    public static void change(int value) {
        value = 20;
    }

    public static void main(String[] args) {
        int number = 10;
        change(number);

        System.out.println(number); // 10
    }
}
```

`change(number)`를 호출할 때 `number`의 값 `10`이 복사되어 `value`에 들어간다.

메서드 안에서 `value = 20`으로 바꿔도, 호출한 쪽의 `number`가 바뀌는 것은 아니다.

## 참조 타입 예시 - 재할당은 반영되지 않는다

```java
class Person {
    String name;

    Person(String name) {
        this.name = name;
    }
}

public class ReferenceValueExample {
    public static void changePerson(Person person) {
        person = new Person("lee");
    }

    public static void main(String[] args) {
        Person p = new Person("kim");
        changePerson(p);

        System.out.println(p.name); // kim
    }
}
```

`p`에는 `Person("kim")` 객체를 가리키는 참조값이 들어 있다.

`changePerson(p)`를 호출하면 그 참조값이 복사되어 매개변수 `person`에 들어간다.

따라서 처음에는 `p`와 `person`이 같은 객체를 가리킨다.

하지만 메서드 안에서 `person = new Person("lee")`를 실행하면, 매개변수 `person`만 새 객체를 가리키게 된다. 호출한 쪽의 `p`는 여전히 기존 `Person("kim")` 객체를 가리킨다.

## 참조 타입 예시 - 객체 내부 상태 변경은 반영된다

```java
class User {
    String name;

    User(String name) {
        this.name = name;
    }
}

public class ObjectStateExample {
    public static void changeName(User user) {
        user.name = "lee";
    }

    public static void main(String[] args) {
        User u = new User("kim");
        changeName(u);

        System.out.println(u.name); // lee
    }
}
```

이 경우에도 매개변수 `user`에는 참조값의 복사본이 들어간다.

다만 `u`와 `user`가 같은 객체를 가리키는 상태에서 `user.name = "lee"`로 객체 내부 상태를 바꿨기 때문에, 호출한 쪽에서도 변경된 상태를 볼 수 있다.

즉, Java가 Call by Reference라서 바뀐 것이 아니라, 복사된 참조값을 통해 같은 객체에 접근했기 때문에 바뀐 것이다.

## 포인터 연산 제거와 캡슐화

Java는 포인터 연산을 없앴다.

주소값을 직접 조작할 수 없기 때문에 원본 객체의 상태를 바꾸려면 멤버 메서드를 통하거나, 접근 가능한 필드에 접근해야 한다. 이 구조는 객체 내부 상태를 외부에서 무분별하게 조작하는 것을 줄이고 [[OOP 4대 원칙|캡슐화]]와 연결된다.

## 관련 개념

- [[Java 문법]]
- [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]
- [[OOP 4대 원칙]]
