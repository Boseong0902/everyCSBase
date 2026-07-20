# Interned String

`String`은 값을 수정하지 않고 새 객체를 만들어 반환하는 불변 객체다.

문자열 비교에서는 `equals()`와 `==`를 구분해야 한다.

- `equals()`: 값 비교
- `==`: 참조값 비교

## String 생성 방식

### 리터럴

```java
String a = "HARIBO";
```

리터럴 방식으로 문자열을 만들면 JVM은 String Constant Pool에 같은 문자열 리터럴이 있는지 먼저 확인한다.

- 있으면 Pool에 있는 동일 객체의 참조를 반환한다.
- 없으면 String Constant Pool에 새 리터럴 객체를 저장한다.

따라서 두 참조 변수에 같은 문자열 리터럴을 넣으면 `==` 비교가 `true`가 될 수 있다.

### new

```java
String a = new String("HARIBO");
```

`new`를 사용하면 String Pool과 무관하게 힙에 새 객체를 생성한다.

## valueOf()

`String.valueOf()`는 파라미터를 문자열로 변환한다.

내부적으로 `toString()`을 호출할 수 있고, 이미 문자열인 경우 같은 객체를 반환할 수 있다.

## intern()

`intern()`은 문자열을 강제로 String Pool 기준으로 맞추는 메서드다.

```java
String a = new String("HARIBO");
String b = a.intern();
String c = "HARIBO";

System.out.println(a == c); // false
System.out.println(b == c); // true
```

동작은 다음과 같다.

- 같은 값이 Pool에 있으면 Pool에 있는 객체의 참조를 반환한다.
- 없으면 Pool에 등록한 뒤 그 참조를 반환한다.

## 관련 개념

- [[String, StringBuffer, StringBuilder]]
- [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]
