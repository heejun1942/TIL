#  Spring: 2nd



### 1. Thymeleaf

> 스프링 부트에서 권장하는 HTML Template
>
> Controller에서 View로 넘겨준 Model을 이용하여 데이터 출력

```html
<!--안써줘도 작동은 함-->
<html xmlns:th="http://www.thymeleaf.org">
    
    <!-- 두 가지 방법이 있음 -->
    <p>[[${user.userId}]]</p>
    <p th:text="${user.userId}"></p>
</html>
```



- 요즘은 jsp대신 Tymeleaf를 쓰는 것을 권장.
- 반복문 사용 가능
- 조건문, 삼항연산자, swich 사용 가능



### 2. Session

> 클라이언트에 대한 정보를 **서버에 저장**할 수 있는 공간
>
> 서버에서 클라이언트를 알기위해 쿠키를 부여하며, 접속 시 발급

- stateless: http & https 모두 상태를 기억하지 않는다.

  즉, 로그인하여도 새로고침하면 풀림.  >  Session 개념 등장

- 특정 시간이 경과하면 세션이 만료되도록 지정할 수 있음.

- 세션은 서버에, **쿠키**는 클라이언트에 존재한다.

  (캐시는 용량이 큰 미디어 파일을 기억하는 것)

- 쿠키 삭제 방법: 개발자도구 > application > cookies 삭제

  

[예제] 로그인 세션 존재 확인하기

```java
package com.heejun.basic.controller;

import javax.servlet.http.HttpSession;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import com.heejun.basic.model.User;

@Controller
public class SessionController {
	@GetMapping("/login")
	public String login() {
		return "login";
	}

	@PostMapping("/login")
	public String loginPost(User user, HttpSession session) {
		session.setAttribute("user", user);
        //해당 주소로 보내버림
		return "redirect:/main";
	}

	@GetMapping("/main")
	public String main() {
		return "main";
	}
}
```

```java
package com.heejun.basic.model;

import lombok.Data;

@Data
public class User {
	private String userId;
	private String userPw;
}
```

```html
<!--login.html-->

<body>
	<form action="/login" method="post">
		ID : <input type="text" name="userId"><br> PW : <input
			type="password" name="userPw"><br> <input type="submit"
			value="로그인">
	</form>
</body>
```

```html
<!--main.html-->

<body>
	<p th:if="${session.user} != null"
		th:text="${session.user.userId} + '님 반갑습니다.'"></p>
	<p th:unless="${session.user} != null">로그인되어 있지 않습니다.</p>
</body>
```



### 3. AOP

> 객체지향 프로그래밍(OOP)을 적용하여도 핵심기능과 부가 기능(로깅, 보안 등)을 분리해서 모듈화하는 것은 매우 여렵다. 이러한 문제를 AOP로 해결할 수 있다.
>
> AOP는 핵심기능에서 부가적인 기능을 분리하며, 분리한 부가기능을 애스팩트(Aspect)라는 모듈형태로 만들어서 설계하고 개발하는 방법이다.

<img src="https://user-images.githubusercontent.com/58925328/71446715-b5996600-2769-11ea-90fc-1842486d9088.png" width=75% />



- Aspect = Advice + PointCut
  - Advice: 부가기능을 정의한 코드
  - PointCut: 어드바이스를 적용할 타겟의 메서드를 선별하는 정규표현식으로, execution으로 시작.
  - Target: 핵심기능을 담고 있는 모듈로, 부가기능을 부여할 대상
  - Join Point (조인포인트): 어드바이스가 적용될 수 있는 위치. 타겟 객체가 구현한 인터테이스의 모든 메서드는 조인 포인트가 된다.
  - Weaving(위빙): 부가기능을 삽입하는 과정을 뜻함. AOP가 핵심기능 코드에 영향을 주지 않으면서 부가기능을 추가할 수 있도록 해주는 핵심적인 처리과정이다.

- 구분된 애스펙트를 런타임 시에 필요한 위치에 동적으로 참여하게 할 수 있다.

<img src="https://user-images.githubusercontent.com/58925328/71446787-83d4cf00-276a-11ea-8b37-421d28029fd0.jpeg" width=80% align="center"/>



- execution() : PoingCut 표현식으로, Advice를 적용할 메소드 지정. 

  - "*"는 모든 값을 의미

    ".."은 0개 이상 의미

  - execution(* some\*(\*,*)): 메서드 이름이 some으로 시작하고, 파라미터가 2개인 메서드 호출

    execution(String com.spring.aop.\*.\*()): aop패키지 내의 String을 반환하고 파라미터가 없는 메서드 호출

```java
package com.ggoreb.basic.aspect;
import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.springframework.stereotype.Component;
import lombok.extern.slf4j.Slf4j;
@Slf4j
@Aspect
@Component
public class ControllerAspect {
 @Before(value = "execution (* com.ggoreb.basic.controller.*.*(..))")
 public void onBeforeHandler(JoinPoint joinPoint) {
 log.debug("@Before run");
 }
 @After(value = "execution (* com.ggoreb.basic.controller.*.*(..))")
 public void onAfterHandler(JoinPoint joinPoint) {
 log.debug("@After run");
 }
 @AfterReturning(value = "execution (* com.ggoreb.basic.controller.*.*(..))"
 , returning = "data")
 public void onAfterReturningHandler(JoinPoint joinPoint, Object data) {
 if(data != null) {
 log.debug(data.toString());
 }
 log.debug("@AfterReturning run");
 }
}
```



### 4. ControllerAdvice

> @ControllerAdvice는 모든 @Controller 즉, 전역에서 발생할 수 있는 예외를 잡아 처리해주는 annotation.
>
> @ExceptionHandler가 하나의 클래스에 대한 것

- 

