# Spring boot

웹애플리케이션 제작

spring.io/tools > Spring Tool Suite 4 다운 > cmd에서 `java -jar spring` `+tab`



## 1. controller 만들기

> Spring에서 컨트롤러를 지정해주기 위한 어노테이션: @RestController, @Controller
>
> - 차이점은 HTTP Response Body가 생성되는 방식임

`@RestController`: 주용도는 Json/Xml 형태로 객체 데이터를 반환

`@Controller`: 주로 View를 반환하기 위해 사용 > 데이터를 반환하기 위해 @ResponseBody 어노테이션을 활용





@GetMapping





응답처리

html  	public *String* home()

JSON	 public *Map* home()



@Controller

@Slf4j

@RequestMapping



@ResponseBody는 JSON으로 출력

​	@GetMapping에서 가능(Map, DTO, List)



String은 데이터를 담지않음 >json 안됨





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



