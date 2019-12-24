### 응답 

- HTML: String, Map, void ...

- JSON: 복합 데이터 + @ResponseBody

​			또는 복합 데이터 + @RestController



### 요청

- @RequestParam: ?뒤에 파라미터 지정. 컨트롤러 메소드의 인자명과 동일. 

- @ModelAttibute: 클래스의 변수명. 모델 클래스의 변수명과 동일. 클래스가 만들어져 있어야함. 



### github올리기

basic > 오른쪽마우스 >  team > share project

받아오기

import > git > 

삭제 후 다시 import?



HTTP

https

- stateless: http&https 모두 상태를 기억하지 않음

  새로고침하면 로그인이 풀림.. > 세션 개념 등장

  request responds

### Session

​	세션은 서버에, 쿠키는 클라이언트에!

​	서버에서 티켓발급(쿠키) : 서버에서 클라이언트를 알기위해 부여 (접속을 할 때 발급받음)

​	개발자도구 > application > cookies 삭제하면 로그인이 풀림. 

​	세션만료: 특정 시간 경과하면 티켓회수

​	(캐시: 용량이 큰 미디어파일을 기억하는 것?)



### AOP

성능 테스트: 어디서 정체가 일어나는지

트랜잭션 처리: 은행에서 현금인출기 느낌. 도 아니면 모. 중간에 오류가 나면 처음부터 시작 (전부 취소/저장x).

임시저장을함.  

​	IoC/DI (Inversion of Control / Dependency Injection): 제어가 역전됨/의존성주입.

​	AOP



```java
// ~~.*.*(..) 패키지 내의 모든 클래스의 모든 메소드
@Before(value = "execution (* com.ggoreb.basic.controller.*.*(..))")
```



### AOP/ Filter/ Interceptor의 차이점

AOP: 어떠한 클래스든, 어떠한 메소드든 대상. 젤 강력한 파워를 가짐(1순위)

Filter:  접속하는 주소(url)를 대상. 반드시 웹서버가 존재하는 곳에서만 동작.

Interceptor:  접속하는 주소(url)를 대상.

- filter와 Interceptor은 하는 일이 똑같. 차이점은 Filter는 자바의 고유기능. Interceptor는 스프링의 기능.



@Configuration



filter > interceptor > aop 순으로 동작



### JPA

repository(저장소)가 데이터베이스의 정보를 입력, 삭제, 조회, 수정을 할 수 있다.

데이터베이스 종류에 종속적이지 않음.



@Entity:  JPA가 이파일을 참조해서 데이터베이스로 만듬.