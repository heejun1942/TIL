# Spring Summary



## 1. 프로젝트 생성

- Spring Boot DevTools: 서버 재시작 없이 수정사항 적용
- Lombok: 변수의 set, get 메소드 자동 생성
- Spring Data JPA: 데이터베이스 템플릿
- H2 Database: 데이터 베이스
- Thymeleaf: 뷰 템플릿(HTML)
- Spring Web: 웹 프로젝트



## 2. Ajax

```html
<!--버튼 클릭시 form태그 submit 시키기-->
<script>
		$("#complete").click(function() {
			$("form").submit();
			return false;
		});
</script>
```

```html
<!--버튼 클릭시 페이지(location) 이동-->
<script>
		$("#write").click(function() {
			location = "/board/write";
			return false;
		});
</script>
```

```html
<!--주소에 변수를 사용하기 (@PathVariable로 받음)-->
<script>
	$("#update").click(function() {
		location = "/board/update/" + [[${board.id}]];
		return false;
	});
</script>
```





## 3. 데이터 주고받기

### 1) Controller에서 View로 데이터 보내기

`model.addAttribute("변수명", "값")`: View로 넘길 데이터



### 2) 클라이언트에게 데이터 받기

@PathVariable: 주소에 {변수명} 형식으로 지정

@RequestParam: 파라미터 종류 및 개수에 상관없이 편하게 사용.

@ModelAttribute: model 객체와 연계하여 활용



```java
//주소로 넘어옴. 여기서는 ajax로..
@GetMapping("/board/{id}")
public String boardView(@PathVariable("id") long id, Model model) {
	Optional<Board> data = boardRepository.findById(id);
	Board board = data.get();
	model.addAttribute("board",board);
	return "board/view";
}
```

```java
// form태그로 user의 key에 대한 값을 받음.
@PostMapping("/signup")
public String signupPost(@ModelAttribute User user) {
	userRepository.save(user);
	return "redirect:/";
}
```

```java
// 방법1
@GetMapping("req/param1")
public String param1( @RequestParam("name") String name, 
                     @RequestParam("age") String age) {
	return name + ", " + age;
}

// 방법2
@GetMapping("req/param2")
public String param2(@RequestParam Map<String, Object> map) {
	return map.toString();
}
```



### 3) RestTemplate: Open API 데이터 받기

> HTTP통신에 유용하게 사용할 수 있는 라이브러리
>
> JSON / XML 형식의 응답결과에 대해 처리 지원



(1) String으로 받기

```java
//String도 @ResponseBody 해줘야함

@ResponseBody
@GetMapping("/movie")
public String movie() {
	RestTemplate rq = new RestTemplate();
	String result = rq.getForObject( "http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchWeeklyBoxOfficeList.json?key=430156241533f1d058c603178cc3ca0e&targetDt=20191229", String.class);
	return result;
}

```



(2) **Map**으로 받기 (파싱하려면 요걸로!)

```java
@ResponseBody
@GetMapping("/movie")
public Map movie() {
	RestTemplate rq = new RestTemplate();
	Map result = rq.getForObject(		"http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchWeeklyBoxOfficeList.json?key=430156241533f1d058c603178cc3ca0e&targetDt=20191229", Map.class);
	return result;
}
```



(3) HTML로 출력하기

```java
// Map으로 받음
@GetMapping("/movie")
public String movie(Model model) {
	RestTemplate rq = new RestTemplate();
	Map<String, Object> result = rq.getForObject(		"http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchWeeklyBoxOfficeList.json?key=430156241533f1d058c603178cc3ca0e&targetDt=20191229", Map.class);
	model.addAttribute("movies",result);
	return "movie";
}
```

```html
<div th:each = "movie : ${movies['boxOfficeResult']['weeklyBoxOfficeList']}">
<p th:text="${movie.movieNm}"></p>
</div>
```

 



#### [참고]

Map<String, Object>: Value 값으로 한가지로 정해지지 않고 여러 형태의 Collection을 넣고 싶다면, Value를 **Collection의 최상위 클래스인 Object로 지정** 해주면 된다.