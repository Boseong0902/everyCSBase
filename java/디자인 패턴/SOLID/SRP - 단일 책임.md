# SRP - 단일 책임

하나의 클래스는 하나의 책임만 가진다

- 높은 가시성과 유지보수성을 위함
- 서비스, 컨트롤러 등등 계층 상관 없이 항상 유지해야될 원칙
- 보통 클래스를 설명할 때 '또한' 이 필요하면 단일 책임 원칙을 위배한 것이다

다음 두 예시는 직사각형 넓이를 구하고, 이를 여러 단위로 환산하는 기능을 구현하는 코드이다.

## 따르지 않는 경우

```java
public class RectangleAreaCalculator {
    private static final double INCH_TERM = 0.025;

    private final int width;
    private final int height;

    public RectangleAreaCalculator(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public int area() {
        return width * height;
    }

    public double metersToInches(int area) {
        return area / INCH_TERM;
    }
}
```

이런 경우, 이 클래스의 기능을 설명하자면,

사각형의 넓이를 계산 또한 미터 단위를 인치 단위로 변환 -> 즉, 단일 책임 원칙 위반

## 따르는 경우

```java
public class RectangleAreaCalculator {
    private final int width;
    private final int height;

    public RectangleAreaCalculator(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public int area() {
        return width * height;
    }
}

public class AreaConvertor {
    private static final double INCH_TERM = 0.0254d;
    private static final double FEET_TERM = 0.3048d;

    public double metersToInches(int area) {
        return area / INCH_TERM;
    }

    public double metersToFeet(int area) {
        return area / FEET_TERM;
    }
}
```

## 왜?

각 클래스를 책임 단위로 분리하기 위함

책임 단위로 분리해야되는 이유는?

코드 재사용성 및 유지보수성

- 특정 목적을 위한 코드 수정이 다른 범위에도 영향을 미치는 것을 방지하기 위함
- 하나의 기능, 책임 단위로 분리함으로써 해당 기능이 필요한 다른 곳에서도 해당 클래스를 재사용 할 수 있음

## 관련 개념

- [[SOLID]]
- [[OCP - 개방-폐쇄]]
- [[객체지향 프로그래밍의 개념 이해]]

