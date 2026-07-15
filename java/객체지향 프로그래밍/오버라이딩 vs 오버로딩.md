# 오버라이딩 vs 오버로딩

## 오버라이딩

동일한 이름과 시그니처를 가지면서 다르게 동작하는 2개 이상의 메서드를 작성하는 것을 의미함

해당 메서드는 static, private, final 메서드이면 안됨

## 오버라이딩이 불가능한 메서드

### static

static -> 메서드 영역에 할당

해당 메서드가 특정 인스턴스가 아닌, 클래스 자체에 귀속되도록 해줌

따라서 객체를 많이 생성해도 모든 객체들이 딱 하나의 메서드만 사용하고 공유함

new 연산자로 객체를 만들지 않아도, 클래스명.메서드명() 으로 바로 호출 가능

### private

private - 해당 클래스 내부에서만 접근이 가능(힙 영역에 할당)

### final

final - 변경 불가능(힙 영역에 할당)

자식 클래스에서 오버라이딩 불가능

## static 메서드와 오버라이딩

public static void main(String[] args) 로 선언하는 main메서드 또한 오버라이딩이 불가능하다

static이 아닌 메서드를 static 메서드로 오버라이드 하거나 그 반대의 경우는 불가능하다

런타임 다형성은 [힙 영역에 생성된 실제 객체의 타입을 보고 메서드를 동적으로 호출하는 것] 이다

여기서 만약 부모의 메서드를 자식이 static으로 바꿔버리면, `Parent p = new Child();` 등의 코드를 사용할 때, 컴파일 에러 발생함

런타임 시점에 힙 영역에 자식 객체가 주입되어 JVM이 그 객체에 접근하지만, 해당 메서드는 메서드 영역에 static으로 만들어 놓음

따라서 이에 대한 참조 방법이 막히게 됨 -> 이걸 컴파일 에러로 막음

반대의 경우, 컴파일 시점에서 보면 부모 클래스에서 해당 메서드를 static으로 선언했고,

참조 변수의 타입은 부모 클래스를 사용할거니까 부모 타입 참조 변수를 보고 해당 메서드를 보면 바로 메서드 영역으로 가게 되지만,

정작 자식 클래스 객체에서 해당 메서드를 오버라이딩한 메서드는 힙에 정의되어있으므로 참조관계가 꼬이게 된다

```java
// 부모 클래스
class Parent {
    public static void print() { ... }
}

// 자식 클래스
class Child extends Parent {
    public void print() { ... } // 컴파일 에러 발생 지점
}

Parent p = new Child();
p.print();
```

## 오버라이딩과 런타임 다형성

메서드 오버라이딩은 상속 혹은 런타임 다형성에 사용된다

추상 클래스 혹은 인터페이스에서 계약한 메서드를 구현 클래스들에서 구현한 상황에서

해당 객체들을 추상 클래스나 인터페이스 타입으로 매개변수를 선언하면,

런타임 시점에 해당 매개변수에 어떤 구현 클래스들의 객체가 들어가는지가 정해짐에 따라

그 메서드의 동작이 결정된다 -> 이게 바로 런타임 다형성

```java
interface Payment {
    void pay(int amount);
}

class KakaoPay implements Payment {
    @Override
    public void pay(int amount) {
        System.out.println("카카오페이로 " + amount + "원 결제합니다. (라이언 이모티콘 발송)");
    }
}

class NaverPay implements Payment {
    @Override
    public void pay(int amount) {
        System.out.println("네이버페이로 " + amount + "원 결제합니다. (1% 포인트 적립)");
    }
}

class Shop {
    public void processOrder(Payment paymentSystem, int price) {
        System.out.println("[주문 처리 시작]");
        paymentSystem.pay(price);
    }
}
```

이를 통해 해당 인터페이스를 구현하는 새로운 구현 클래스가 추가되더라도, 주입받는 클래스(Shop)를 수정할 필요가 없다 -> OCP 충족, 즉 확장성 고려

## 오버로딩

같은 이름이지만, 다른 시그니처와 그에 따른 다른 기능을 하도록 2개 이상의 메서드를 작성하는 것

static 여부는 모든 오버로딩 된 메서드가 동일해야됨 -> 모든 오버로딩 된 메서드가 static이던가, 모든 오버로딩 된 메서드가 static이 아니던가

시그니처가 다르다 -> 인수의 구성이 다르다

따라서 인수의 구성이 동일하지만, 반환 타입이 다른것은 오버로딩이 아니다(애초에 문법적으로 컴파일 에러)

오버로딩된 메서드들은 컴파일 시점에 어떤 메서드가 호출될지 명확히 결정됨 -> 런타임 다형성 아님

## 공변 메서드 오버라이딩이란?

오버라이딩 메서드는 수퍼 클래스의 반환 타입의 하위 타입을 반환할 수 있다.

```java
class Animal {}
class Dog extends Animal {}

class AnimalClinic {
    public Animal heal() {
        return new Animal();
    }
}

class DogClinic extends AnimalClinic {
    @Override
    public Dog heal() {
        return new Dog();
    }
}
```

이게 없다면? 매번 메서드 호출 시마다 다운 캐스팅이 필요해짐

```java
DogClinic clinic = new DogClinic();
Dog myDog = (Dog) clinic.heal();
```

## 오버라이딩 및 오버로딩 메서드에서 예외처리 제한 사항은?

오버라이딩

자식 클래스에서 부모 클래스의 메서드를 오버라이딩 할 때, throws로 던질 수 있는 예외는 부모 메서드가 던지는 예외보다 클 수 없다

-> LSP

## 관련 질문

- 오버로딩과 오버라이딩과 관련한 규칙은?
- 메서드 오버라이딩과 오버로딩의 주요한 차이점은?
- static이나 private 메서드를 오버라이드 할 수 있나?
- final 메서드를 오버라이드 할 수 있는가?
- static 메서드를 오버로드 할 수 있는가?
- 오버라이딩 메서드의 인수 목록을 변경해도 되는가?

## 관련 개념

- [[정적 다형성과 런타임 다형성]]
- [[interface]]
- [[인터페이스와 추상 클래스]]
- [[static, final 키워드]]
- [[자바의 데이터 저장소 - 메서드 영역, 스택 영역, 힙 영역]]
- [[OCP - 개방-폐쇄]]
- [[LSP - 리스코프 치환]]

