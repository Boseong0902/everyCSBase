# interface

인터페이스는 객체가 외부에 제공해야 하는 기능의 계약을 정의한다. 구현 클래스는 이 계약을 충족해야 하며, 각 기능의 구체적인 구현 방식은 클래스마다 달라질 수 있다.

이를 통해 추상화 | 다형성 | 느슨한 결합과 유지보수성을 보장할 수 있다

## 예시

```java
public interface car {
    public void accelerate();
    public void slowDown();
    public void turnRight();
    public void turnLeft();
    public void goToBack();
    public void getRemainEnergy();
    public void recharge();
}

public class gasolinCar implements car {
    @Override
    public void accelerate() {};

    @Override
    public void slowDown();

    @Override
    public void turnRight();

    @Override
    public void turnLeft();

    @Override
    public void goToBack();

    @Override
    public void getRemainEnergy();

    @Override
    public void recharge();
}

public class electricCar implements car {
    @Override
    public void accelerate();

    @Override
    public void slowDown();

    @Override
    public void turnRight();

    @Override
    public void turnLeft();

    @Override
    public void goToBack();

    @Override
    public void getRemainEnergy();

    @Override
    public void recharge();
}
```

## 추상화

여기서 전기차든 내연차든 뭐든간에 호출해야되는 상황이라고 해보자. 만약 인터페이스로 메서드들을 안묶었으면 각각이 메서드 이름을 확인해봐야된다.

근데 인터페이스로 묶음으로써 그 내부를 확인 안해도 해당 기능이 electricCar, gasolinCar 모두에 다 구현이 되어있음을 알고 호출부에서 편하게 사용이 가능하다

## 다형성

인터페이스는 런타임 다형성의 기준 타입으로 사용할 수 있다

```java
public static void main(String[] agrs) {
    Car car = new electricCar();
    car.accelerate();
}
```

위 코드에서, 컴파일 시점에 저 car가 gasolinCar일지, electronicCar일지 모른다.

런타임 시점에서야 정해진다

이 흐름은 [[정적 다형성과 런타임 다형성]] 중 런타임 다형성에 해당한다.

## 느슨한 결함과 유지보수성

구체 클래스를 직접 선언하면 결합도가 높아진다.

```java
public class Driver {
    private final electricCar car = new electricCar();
}
```

이러면 Driver가 electricCar에 고정되어 있기 때문에 gasolinCar로 교체하려면 코드를 바꿔야 된다

```java
public class Driver {
    private final car car;

    public Driver(car car) {
        this.car = car;
    }
}
```

이러면 컴파일 시점에선 어떤 자동차인지 모르므로 결합도가 낮아진다.

## 관련 개념

- [[Java]]
- [[Java 문법]]
- [[객체지향 프로그래밍의 개념 이해]]
- [[인터페이스와 추상 클래스]]
- [[정적 다형성과 런타임 다형성]]
- [[OCP - 개방-폐쇄]]
- [[ISP - 인터페이스 분리]]
- [[DIP - 의존 관계 역전]]
