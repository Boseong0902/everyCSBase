# DIP - 의존 관계 역전

DIP는 고수준 모듈(비지니스 로직)이 저수준 구현체에 직접 의존하지 않고, 둘 다 추상화(인터페이스)에 의존하도록 설계하라는 원칙이다.

즉, 핵심 비지니스 로직이 구체 클래스의 생성 방식이나 구현 세부사항에 묶이지 않게 만드는 것이다.

## 핵심 규칙

- 고수준 모듈은 저수준 모듈에 의존하면 안 된다.
- 둘 다 추상화에 의존해야 한다.
- 추상화는 세부사항에 의존하면 안 된다.
- 세부사항이 추상화에 의존해야 한다.

여기서 고수준 모듈은 정책이나 비지니스 흐름을 담은 코드이고, 저수준 모듈은 DB, 외부 API, 파일 시스템, 메시지 전송 같은 구체 구현이다.

## 잘못 이해하기 쉬운 점

DIP는 무조건 “상속 계층에서 가장 위 부모 클래스에 의존하라”는 뜻이 아니다.

예를 들어 `Animal -> Bird -> PredatorBird -> Eagle` 같은 상속 구조가 있을 때, 단순히 `Animal`에 의존한다고 해서 항상 좋은 설계가 되는 것은 아니다. 호출하는 코드가 실제로 필요한 기능이 `fly()`라면 `Animal`은 너무 넓거나 부정확한 추상화일 수 있다.

DIP에서 중요한 것은 “가장 위 타입”이 아니라 “사용자가 필요로 하는 역할을 표현하는 추상화”다.

```java
interface Flyable {
    void fly();
}
```

비행 기능만 필요하다면 `Animal`보다 `Flyable`에 의존하는 편이 더 명확할 수 있다.

## DIP를 어긴 예시

```java
class EmailSender {
    void send(String message) {
        System.out.println("email: " + message);
    }
}

class OrderService {
    private final EmailSender emailSender = new EmailSender();

    void order() {
        // 주문 처리
        emailSender.send("주문이 완료되었습니다.");
    }
}
```

이 코드에서 `OrderService`는 고수준 비지니스 로직이다. 그런데 구체 구현체인 `EmailSender`를 직접 생성하고 사용한다.

문제는 다음과 같다.

- 알림 방식을 SMS나 카카오 알림으로 바꾸려면 `OrderService`를 수정해야 한다.
- 테스트할 때 실제 `EmailSender` 대신 가짜 구현체를 넣기 어렵다.
- 주문 로직이 알림 구현 방식에 묶인다.

## DIP를 적용한 예시

```java
interface NotificationSender {
    void send(String message);
}

class EmailSender implements NotificationSender {
    @Override
    public void send(String message) {
        System.out.println("email: " + message);
    }
}

class SmsSender implements NotificationSender {
    @Override
    public void send(String message) {
        System.out.println("sms: " + message);
    }
}

class OrderService {
    private final NotificationSender notificationSender;

    OrderService(NotificationSender notificationSender) {
        this.notificationSender = notificationSender;
    }

    void order() {
        // 주문 처리
        notificationSender.send("주문이 완료되었습니다.");
    }
}
```

이제 `OrderService`는 `EmailSender`나 `SmsSender` 같은 구체 구현체를 모른다. 오직 `NotificationSender`라는 역할에만 의존한다.

구현체 교체는 외부에서 결정한다.

```java
NotificationSender sender = new EmailSender();
OrderService orderService = new OrderService(sender);
```

테스트에서는 가짜 구현체를 넣을 수도 있다.

```java
class FakeSender implements NotificationSender {
    String sentMessage;

    @Override
    public void send(String message) {
        this.sentMessage = message;
    }
}
```

## 의존 관계가 역전된다는 의미

DIP를 적용하기 전에는 고수준 정책이 저수준 구현체를 직접 바라본다.

```text
OrderService -> EmailSender
```

DIP를 적용하면 고수준 정책과 저수준 구현체가 모두 추상화를 바라본다.

```text
OrderService -> NotificationSender <- EmailSender
                                      <- SmsSender
```

그래서 의존 방향이 “구체 구현체 쪽”으로 흐르지 않고, 추상화 쪽으로 모인다.

## OCP와의 관계

DIP는 [[OCP - 개방-폐쇄]]를 가능하게 만드는 대표적인 방법이다.

`OrderService`가 `NotificationSender`에만 의존하면, 새로운 알림 방식이 필요할 때 `PushSender` 구현체를 추가하면 된다. 기존 `OrderService` 코드를 수정하지 않아도 되므로 확장에는 열려 있고 변경에는 닫힌 구조가 된다.

## Spring에서의 DIP

Spring의 [[DI와 IoC]]는 DIP를 구현하기 쉽게 해주는 도구다.

개발자는 고수준 모듈이 인터페이스에 의존하도록 만들고, 어떤 구현체를 넣을지는 스프링 컨테이너가 외부에서 주입한다.

```java
@Service
class OrderService {
    private final NotificationSender notificationSender;

    OrderService(NotificationSender notificationSender) {
        this.notificationSender = notificationSender;
    }
}
```

여기서 중요한 것은 Spring을 쓰면 자동으로 DIP가 되는 것이 아니라, 코드가 먼저 추상화에 의존하도록 설계되어 있어야 한다는 점이다.

## DIP의 장점

- 상위 비지니스 로직이 구현체 교체에 덜 흔들린다.
- 테스트에서 fake, stub, mock 구현체를 넣기 쉽다.
- 새로운 구현체를 추가해도 기존 고수준 로직을 덜 수정한다.
- 구현 세부사항이 핵심 정책 안으로 새어 들어오는 것을 줄인다.

## 관련 개념

- [[SOLID]]
- [[interface]]
- [[OCP - 개방-폐쇄]]
- [[DI와 IoC]]
- [[전략]]
