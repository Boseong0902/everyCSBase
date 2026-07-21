# equals와 ==

Java에서 `==`와 `equals()`는 둘 다 비교에 사용되지만 비교 기준이 다르다.

## == 비교

`==`는 피연산자의 값 자체를 비교한다.

기본형에서는 실제 값을 비교한다.

```java
int a = 10;
int b = 10;

System.out.println(a == b); // true
```

참조형에서는 객체의 내용이 아니라 참조값을 비교한다. 즉, 두 변수가 같은 객체를 가리키는지를 본다.

```java
User a = new User("kim");
User b = new User("kim");

System.out.println(a == b); // false
```

두 객체의 `name` 값은 같지만, `new`로 서로 다른 객체를 만들었기 때문에 참조값이 다르다.

## equals() 비교

`equals()`는 객체의 논리적 동등성을 비교하기 위해 사용한다.

다만 `Object`의 기본 `equals()`는 `==`와 동일하게 참조값을 비교한다. 그래서 값 기준 비교가 필요하면 직접 오버라이딩해야 한다.

```java
class User {
    private final String name;

    User(String name) {
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) {
            return true;
        }
        if (!(o instanceof User)) {
            return false;
        }
        User user = (User) o;
        return name.equals(user.name);
    }
}
```

이렇게 오버라이딩하면 서로 다른 객체라도 `name`이 같으면 논리적으로 같은 객체로 볼 수 있다.

## equals()와 hashCode()

`equals()`를 오버라이딩할 때는 보통 `hashCode()`도 함께 오버라이딩해야 한다.

Java의 해시 기반 컬렉션은 먼저 `hashCode()`로 버킷을 찾고, 같은 버킷 안에서 `equals()`로 실제 동등성을 확인한다.

대표적인 예시는 다음과 같다.

- `HashSet`
- `HashMap`
- `LinkedHashSet`
- `LinkedHashMap`

## 객체 비교 2단계 프로세스
1. 데이터 추가 시도
2. hashCode() 비교 -> 다르다 -> 다른 객체로 인식 -> 다른 버킷에 저장
	1. hashCode() : 해시 값을 반환
	2. 따라서 해시값을 비교해서 동일하면 동일 버킷에 넣고, 다르면 버킷 자체를 분리
	3. 버킷이 분리된 두 객체는 equals()호출조차 되지 않는다
3. hashCode()값이 같다 -> equals()비교 -> 다르다 -> 다른 객체로 인식(동일 버킷 내 연결 리스트 or 트리 탐색)
	1. 연결 리스트 방식 사용 -> 동일 버킷 내에서 노드 탐색 시간 : O(n)
	2. 따라서 동일 버킷의 노드가 8개가 넘어가면 바로 트리로 전환 -> O(log n)
4. equals()값이 같다 -> 완전 동일한 객체로 인식


## Map에서의 활용

`HashMap`은 key를 찾을 때 `hashCode()`로 버킷을 찾고, `equals()`로 같은 key인지 확인한다.

```java
Map<User, Integer> scores = new HashMap<>();
scores.put(new User("kim"), 100);

System.out.println(scores.get(new User("kim"))); // null
```

`User`가 `equals()`와 `hashCode()`를 제대로 오버라이딩하지 않았다면 `get(new User("kim"))`은 기존 key와 다른 객체로 판단되어 값을 찾지 못한다.

반대로 둘을 `name` 기준으로 오버라이딩하면, 새로 만든 `User("kim")`으로도 기존 값을 찾을 수 있다.

```java
Map<User, Integer> scores = new HashMap<>();
scores.put(new User("kim"), 100);

System.out.println(scores.get(new User("kim"))); // 100
```


## Set에서의 활용

사실 hashSet은 내부적으로 hashMap을 사용해서 구현되어 있기 때문에 두 컬렉션 모두 객체의 동등성을 판단하는 메커니즘이 동일하다
	| hashSet에 데이터를 넣는 것은 hashMap의 Key자리에 데이터를 넣는것과 완전 동일
	| 그럼 hashMap의 value는 어떻게 처리? -> 의미없는 가짜 객체를 넣어놓음

```java
class User {
    private final String name;

    User(String name) {
        this.name = name;
    }
}

Set<User> users = new HashSet<>();
users.add(new User("kim"));
users.add(new User("kim"));

System.out.println(users.size()); // 2
```

위 코드에서 `User`는 `equals()`와 `hashCode()`를 오버라이딩하지 않았다. 그래서 두 객체는 값이 같아 보여도 서로 다른 객체로 취급된다.

```java
class User {
    private final String name;

    User(String name) {
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) {
            return true;
        }
        if (!(o instanceof User)) {
            return false;
        }
        User user = (User) o;
        return name.equals(user.name);
    }

    @Override
    public int hashCode() {
        return name.hashCode();
    }
}

Set<User> users = new HashSet<>();
users.add(new User("kim"));
users.add(new User("kim"));

System.out.println(users.size()); // 1
```

이제 `name`이 같은 두 `User` 객체는 같은 객체로 취급된다.


## 정리

| 비교 방식 | 기본형 | 참조형 |
| --- | --- | --- |
| `==` | 실제 값 비교 | 참조값 비교 |
| `equals()` | 사용 불가 | 기본은 참조값 비교, 오버라이딩하면 논리적 동등성 비교 |

`String`은 이미 `equals()`가 값 기준으로 오버라이딩되어 있다. 그래서 문자열 값 비교는 `==`가 아니라 `equals()`를 사용하는 것이 안전하다.

## 관련 개념

- [[Interned String]]
- [[컬렉션 프레임워크]]
- [[Call by Value]]
- [[캐스팅]]
