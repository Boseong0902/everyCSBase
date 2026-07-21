# Dispatcher Servlet

Dispatcher Servlet은 서블릿 컨테이너에서 HTTP 프로토콜을 통해 들어오는 요청을 가장 앞에서 처리하는 컨트롤러다.

서버가 요청을 각 세부 컨트롤러로 넘기기 전에 공통 처리 작업을 수행하고, 요청에 맞는 컨트롤러로 작업을 위임한다.

## 역할

- HTTP 요청을 가장 앞단에서 받는다.
- 공통 처리 작업을 수행한다.
- 요청 URL과 메서드에 맞는 컨트롤러를 찾는다.
- 실제 세부 컨트롤러에 작업을 위임한다.

Dispatcher Servlet은 웹 요청 흐름의 관문 역할을 한다.

## AOP와의 차이

Dispatcher Servlet도 공통 처리를 할 수 있지만, 기본적으로 웹 요청을 다루는 컴포넌트다.

웹 요청이 없는 `@Scheduled` 배치 작업이나 메시지 큐 리스너에는 Dispatcher Servlet이 관여하지 않는다. 메서드 호출 단위의 공통 관심사 처리가 필요하면 [[스프링 AOP]]가 더 적절하다.

## 관련 개념

- [[Spring]]
- [[스프링 AOP]]
- [[Annotation]]
