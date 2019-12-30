# Spring boot 시작하기

> Spring boot를 사용하여 **웹 애플리케이션**을 제작하자



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

> lombok: 변수의 set, get 메소드를 자동으로 생성해줌 ( **@Data** )

```
java -jar lombok [Tab키 누르기]
```



## 2. controller 클래스 생성

> Spring에서 컨트롤러를 지정해주기 위한 어노테이션. 차이점은 HTTP Response Body가 생성되는 방식임
>

- @Controller: 주로 View를 반환하기 위해 사용 > 데이터를 반환하기 위해 @ResponseBody 어노테이션을 활용

- @RestController: @Controller + @ResponseBody. 리턴값을 뷰리졸버로 매핑하지 않고 그대로 출력함. 주용도는 Json/Xml 형태로 객체 데이터를 반환.

  ( @은 **어노테이션**으로 자바를 위한 주석 )



## 3. 응답

> View는 모델이 가진 정보를 어떻게 표현해야 하는지에 대한 로직을 갖고 있는 컴포넌트. 일반적으로 HTML이며, 엑셀, PDF, 이미지 등을 생성할 수도 있음.
>
> View Resolver는 사용할 뷰 오브젝트를 찾고 생성하는 작업을 함.



#### 3.1 응답 형태

- View 이름 리턴: html파일은 resource > templates에 생성

  ```java
  return login	//login.html 파일 리턴
  ```

- HTML: **String**, Map, void...

- JSON: 복합데이터 + @ResponseBody 또는 @RestController

  - @GetMapping에서 가능(Map, DTO, List)

  - String은 데이터를 담지않음 >json 안됨



**※ 참고**: SpringBoot DevTools: 서버 재기동없이 수정사항 적용

1. build.gradle > Dependencies에 다음을 추가해주자.

```java
implementation "org.springframework.boot:spring-boot-devtools"
```

2. build.gradle에서 오른쪽 마우스 'Refresh Gradle Project' 클릭



#### 3.2 Model 객체 사용법

> Model 객체를 파라미터로 받아서 데이터를 뷰로 넘길 수 있다. (String형으로 줌)

- `model.addAttribute("변수명", "값")`: 뷰로 넘길 데이터

```java
@RequestMapping("/board/view") 
public String view(Model model) { 
    
    // 데이터만 설정이 가능 
    model.addAttribute("id", "hongku");  
    
    return "board/view"; 
}
```

```html
<!--view.html에서 넘겨준 값을 받음-->
<body>
   [[${id}]] 
</body>
```



#### 3.3 ModelAndView 객체 사용법

> 반환값으로 ModelAndView 객체를 반환한다. (인자가 없음)

```java
@RequestMapping("/board/view") 
public ModelAndView content() { 
    
    // 데이터와 뷰를 동시에 설정이 가능 
    ModelAndView mv = new ModelAndView(); 
    mv.setViewName("/board/view");	// 뷰의 이름 
    mv.addObject("id", "hongku");   // 뷰로 보낼 데이터 값 
    
    return mv; 
}
```

```html
<!--view.html에서 넘겨준 값을 받음-->
<body>
   [[${id}]] 
</body>
```



## 4. 요청

#### 4.1 요청 메소드

- @RequestMapping: **View의 요청 경로** 지정

```java
@RequestMapping("/login")
```

- 요청 형태: **GET, POST, PUT, DELETE** (POST는 파라미터가 안보임)

  @GetMapping은 `@RequestMapping(method = RequestMethod.GET)` 의 축약형으로 아래의 두 코드는 같은 의미임. 

  ```java
  @RequestMapping(value="req/get" method = RequestMethod.Get)
  ```

  ```java
  @GetMapping("req/get")
  ```



※ 참고: GET 이외의 메소드를 실험하기 위해서는 Rest Client(Talend API Tester)을 웹스토어에서 설치해줘야함.



#### 4.2 파라미터 받기

> 서버가 클라이언트 값을 받는 방법
>
> - @RequestParam: ?뒤에 파라미터 지정. 컨트롤러 메소드의 인자명과 동일. 
> - @ModelAttibute: 클래스가 만들어져 있어야함. Model에 작성되어 있는 변수/자료형과 파라미터명이 동일하면 자동으로 대입

```
http://localhost:8080/req/param1?key1=a&key2=1
```

※ 클라이언트가 서버로 값을 보내는 방법: form태그



1. @RequestParam 두 가지 방법

   ```java
   //key값이 정해져 있음. 
   //요청된 파라미터의 값이 없는 경우 400 오류 > defaultValue를 지정
   @GetMapping("req/param")
   public String param(
   		@RequestParam("name") String key1,
   		@RequestParam("age") String key2) {
       
   	return key1 + ", " + key2;
   }
   ```

   ```java
   //key가 지정되어있지 않아 자유롭게 인수로 보낼 수 있음
   @GetMapping("req/param")
   public String param2(
   		@RequestParam Map<String, Object> map) {
       
   	return map.toString();
   }
   ```



2. @ModelAttibute

   ```java
   @RestController
   public class RequestController {
   	@GetMapping("req/model")
   	public String model(@ModelAttribute Member member) {
   		return member.toString();
   	}
   }
   ```

   ```java
   package com.heejun.basic.model;
   
   import lombok.Data;
   
   @Data
   public class Member {
   	private String name;
   	private String userId;
   	private String userPassword;
   }
   ```

   

3. @RequestBody: JSON 형태의 파라미터 사용. (GET 방식은 Body 가 존재하지 않기 때문에 반드시 POST 여야 한다 )





## [정리]

1. client, server를 이해하고 어떻게 통신하는지 살펴보자.

2. client가 server를 부르는 형태:get, post,delete,put

3. 응답형태: **html**, 이미지, 파일다운, **JSON**

   - html: return형태는 대부분 String

   - JSON: return형태는 map, array, list, object

     ​			@ResponseBody을 붙임. 또는, @Controller대신 @RestController를 씀

4. 컨트롤러 클래스 제작 순서

   @Controller를 이용해 클래스 생성 > @RequestMapping을 통해 view의 요청 경로 지정 > 요청 처리 메소드 구현 > view 이름 리턴

   ```java
   @Controller // 컨트롤러 지정 
   public class HomeController { 
       // 뷰의 요청 경로 지정 
       @RequestMapping(value = "/welcome", method = RequestMethod.GET) 
    	public String welcome(Model model) {
           
       	// 로직 수행 
           Member member = new Member();
   		member.setUserId("a");
    		member.setName("spring");
    		member.setUserPassword("1234");
           
           // Model 객체를 이용해서, view로 Data 전달 
           model.addAttribute("member", member);
           
           return "welcome"; // 뷰 파일 리턴 
       } 
   }
   ```

   

