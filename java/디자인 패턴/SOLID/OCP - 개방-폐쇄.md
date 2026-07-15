# OCP - 개방-폐쇄

확장에 대해선 개방되어있고, 수정에 대해선 폐쇄되어있으어 햔다

즉, 어떠한 기능적인 변경을 위해선 해당 클래스를 확장하는 형식으로만 구현할 수 있도록 설계해야된다.

## 따르지 않는 경우

```java
public interface Shape {}

public class Rectangle implements Shape {
    private final int width;
    private final int height;
}

public class Circle implements Shape {
    private final int radius;
}

public class AreaCalculator {
    private final List<Shape> shapes;

    public AreaCalculator(List<Shape> shpaes) {
        this.shapes = shapes;
    }

    public double sum() {
        int sum = 0;

        for (Shape shape : shapes) {
            if (shpe.getClass().equals(Circle.class)) {
                sum += Math.PI * Math.pow(((Circle) shape).getRadius(), 2);
            } else if (shape.getClass().equals(Rectangle.class)) {
                sum += ((Rectangle) shape).getHeight()
                    * ((Rectangle) shape).getWidth();
            }
        }

        return sum;
    }
}
```

-> 이 코드는 결국 도형이 추가 될 때 마다 AreaCalculator 클래스 안에서 if-elseif 문의 코드를 추가해야된다.

따라서 이런 경우, interface를 사용한다

## 따르는 경우

```java
public interface Shape {
    public double area();
}

public class Rectangle implements Shape {
    private final int width;
    private final int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height
    }
}

public class Circle implements Shape {
    private final int radius;

    public Circle(int radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * Math.pow(radius, 2);
    }
}

public class AreaCalculator {
    private final List<Shape> shapes;

    public AreaCalculator(List<Shape> shapes) {
        this.shapes = shpaes;
    }

    public double sum() {
        int sum = 0;

        for (Shape shape : shapes) {
            sum += shape.area();
        }

        return sum;
    }
}
```

이러면 추후에 도형이 더 추가되더라도 AreaCalculator 클래스는 수정할 일이 없이, 코드 확장만으로 구현이 가능해진다

## 잘 생각해보자

단일 책임 원칙을 지키는 것과 개방-폐쇄 원칙을 지키는 것의 차이가 뭘까?

SRP(단일 책임 원칙) -> 수직적 구분

- 넓이 구하는 계층
- 단위 수정하는 계층

OCP(개방-폐쇄 원칙) -> 수평적 구분

- 원, 직사각형, 정사각형 등등을 구분

이에 따라서 단일 책임 원칙 은 지켰지만 개방-폐쇄 원칙 은 지키지 못한 코드도 발생하게 된다(정확히 위에서 언급한 예시)

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

여기서 또 meterToCentimeter가 추가되면 AreaConvertor클래스를 수정해야된다.

또한, 아까처럼 List로 일괄적 관리를 위해선 마찬가지로 또다시 if-else()구문을 꺼내야된다

따라서 이또한 interface로 구현하겨나, 혹은 AreaConvertor를 추상클래스로 만들고, 이를 상속받게 하는게 좋은 코드가 된다

## 관련 개념

- [[SOLID]]
- [[SRP - 단일 책임]]
- [[LSP - 리스코프 치환]]
- [[interface]]
- [[정적 다형성과 런타임 다형성]]
