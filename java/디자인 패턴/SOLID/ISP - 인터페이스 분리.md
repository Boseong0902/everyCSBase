# ISP - 인터페이스 분리

불필요한 메서드를 강제로 구현하는 일이 없게 하기 위해서 하나의 인터페이스를 여러 인터페이스로 분리한다

근데 관련은 있는데, 경우에 따라 분리가 필요해보일 때도 있음

## 예시

```java
public interface Connection {
    public void socket();
    public void http();
    public void connect();
}

public class wwwPingConnection implements Connection {
    private final String www;

    public wwwPingConnection(String www) {
        this.www = www;
    }

    @Override
    public void http() {
        System.out.println("Setup an HTTP connection to " + www);
    }

    @Override
    public void socket() {}

    @Override
    public void connect() {
        System.out.println("Connect to " + www);
    }
}
```

위 코드는 socekt 메서드는 필요 없지만, 그렇다고 socketConnection 의 새 클래스를 정의하기엔, connect() 메서드는 두 인터페이스 모두 다 필요하기에 분리하기 애매하다

이런 경우엔 인터페이스 상속을 사용

```java
public interface Connection {
    public void connect();
}

public interface HttpConnection extends Connection {
    public void http();
}

public interface SocketConnection extends Connection {
    public void socket();
}

public class wwwPingConnection implements HttpConnection {
    private final String www;

    public wwwPingConnection(String www) {
        this.www = www;
    }

    @Override
    public void http() {
        System.out.println("Setup an HTTP connection to " + www);
    }

    @Override
    public void connect() {
        System.out.println("Connect to " + www);
    }
}
```

분리 전에는 필요도 없는 `socket()`을 빈 메서드로 구현해야 했지만, `HttpConnection`만 구현하면서 그 강제 구현이 사라졌다.

공통으로 필요한 `connect()`는 상위 인터페이스인 `Connection`에 남겨두었기 때문에 두 계열 모두에서 그대로 쓸 수 있다.

## 관련 개념

- [[SOLID]]
- [[interface]]
- [[DIP - 의존 관계 역전]]

