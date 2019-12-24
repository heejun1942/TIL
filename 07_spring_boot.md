# Spring boot 시작하기

Spring boot를 사용하여 **웹 애플리케이션** 제작



- 통신 흐름 : 클라이언트 요청과 서버 응답

<img src="https://user-images.githubusercontent.com/58925328/71407849-91615a80-267f-11ea-9768-d99c5700c194.PNG" width="80%" />

- 스프링 MVC

<img src="https://user-images.githubusercontent.com/58925328/71411164-a643eb00-268b-11ea-844b-f5f2424a9fd3.PNG" width="80%" />





## 1. 설치

1.1 STS(Spring Tool Suite 4) 설치 

```
java -jar spring [Tab키 누르기]
```



1.2 lombok 다운 

> lombok: 변수의 set, get 메소드를 자동으로 생성해줌

```
java -jar lombok [Tab키 누르기]
```



## 2. controller 클래스 생성

> Spring에서 컨트롤러를 지정해주기 위한 어노테이션. 차이점은 HTTP Response Body가 생성되는 방식임
>
> - @Controller: 주로 View를 반환하기 위해 사용 > 데이터를 반환하기 위해 @ResponseBody 어노테이션을 활용
> - @RestController: @Controller + @ResponseBody. 리턴값을 뷰리졸버로 매핑하지 않고 그대로 출력함. 주용도는 Json/Xml 형태로 객체 데이터를 반환.
>
> ( 참고: @은 **어노테이션**으로 자바를 위한 주석 )



### 2.1 응답 

> View는 모델이 가진 정보를 어떻게 표현해야 하는지에 대한 로직을 갖고 있는 컴포넌트. 일반적으로 HTML이며, 엑셀, PDF, 이미지 등을 생성할 수도 있음.
>
> View Resolver는 사용할 뷰 오브젝트를 찾고 생성하는 작업을 함.

[메소드]

@RequestMapping: 요청에 대해 어떤 메소드가 처리할지를 맵핑

@GetMapping: @RequestMapping(method = RequestMethod.GET) 의 축약형

[응답 형태]

- HTML: String, Map, void...

- JSON: 복합데이터 + @ResponseBody 또는 @RestController

  - @GetMapping에서 가능(Map, DTO, List)

  - String은 데이터를 담지않음 >json 안됨



※ 참고: SpringBoot DevTools: 서버 재기동없이 수정사항 적용

1. build.gradle > Dependencies에 다음을 추가해주자.

```java
implementation "org.springframework.boot:spring-boot-devtools"
```

2. build.gradle에서 오른쪽 마우스 'Refresh Gradle Project' 클릭



### 2.2 요청

- @RequestParam: ?뒤에 파라미터 지정. 컨트롤러 메소드의 인자명과 동일. 

- @ModelAttibute: 클래스의 변수명. 모델 클래스의 변수명과 동일. 클래스가 만들어져 있어야함.





응답처리

html  	public *String* home()

JSON	 public *Map* home()









### 응답방식

1. Html
   - string
2. Json
   - map, array, list, object // @ResponseBody
   - RestController를 사용하면 @ResponseBody를 안써도됨



### Rest Client설치하기

웹스토어에서 Talend API Tester설치



### 응답방식

- HTML -> string



### 서버가 클라이언트 값을 받는 방법

1. RequestParam: 그냥 프로젝트할 때.? 제약 없이 값을 받을 수 있음

2. ModelAttribute: 서버에서 지정한 것만 넘겨야함, 회사에서 선호



HttpServletRequest ..? 옛날방식..

 request.getParameter("name") ...?



@RequestParam..? 서버에서 클라이언트가 전달하는 값을 받음. 2가지 방법이 있음(45p)

```
http://localhost:8080/req/param1?key1=a&key2=1
```

​	※ 클라이언트가 서버로 값을 보내는 방법: form태그



- Thymeleaf(49p)

  medel을 html넘겨주는 코드는 없지만 사용가능.

  요즘은 jsp대신 Tymeleaf를 쓰는 것을 권장.

  - 반복문 쓰는방법
  - 조건문, 삼항연산자, swich 
  - 




바뀌어야하는 값은 controller에서 작동해야함

## [정리]

1. STS 설치

```
java -jar sp [tap키누르기]
```

2. lombok 설치: 변수에대해 set,get메소드를 자동으로 생성

```
java -jar lombok [tap키누르기]
```

3. 컨트롤러 클래스 생성

   - 응답형태임

   메소드(@GetMapping / @RequestMapping)

   @ResponseBody 또는 @RestController

   JSON 또는 HTML



- client, server를 이해하고 어떻게 통신하는지 살펴보자.

  client가 server를 부르는 형태:get, post,delete,put

  응답형태: **html**, 이미지, 파일다운, **JSON**

  ​	return형태: **String**, void, Map 

  ​		(html일땐 대부분 String)

  ​		JONS일땐 @ResponseBody을 붙임

  ​							또는, @Controller대신 @RestController를 씀



