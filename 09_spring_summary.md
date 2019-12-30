- Spring Boot DevTools: 서버 재시작 없이 수정사항 적용
- Lombok: 변수의 set, get 메소드 자동 생성
- Spring Data JPA: 데이터베이스 템플릿
- H2 Database: 데이터 베이스
- Thymeleaf: 뷰 템플릿(HTML)
- Spring Web: 웹 프로젝트







object

ResponseEntity

-getForObject-

Map: 키, 값을 가짐

List:순서에 따라 저장

List\<Map\>: 

List\<object\> : model에 정의되 있어야함.?

Object[]



클래스? 유사한 특징을 지닌 객체들의 속성을 묶어 놓은 집합체

object? 클래스를 사용할 수 있게 실체화한 것

클래스안에 특정 기능을 구현한 것



## Ajax

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







## 데이터 주고받기

### 1. Controller에서 View로 데이터 보내기

`model.addAttribute("변수명", "값")`: View로 넘길 데이터



### 2. 클라이언트에게 데이터 받기

@PathVariable: 주소에 {변수명} 형식으로 지정

@RequestParam: 파라미터 종류 및 개수에 상관없이 편하게 사용.

@ModelAttribute: model 객체와 연계하여 활용



```java
@GetMapping("/board/{id}")
public String boardView(@PathVariable("id") long id, Model model) {
	Optional<Board> data = boardRepository.findById(id);
	Board board = data.get();
	model.addAttribute(board);
	return "board/view";
}
```

```java
@PostMapping("/board/write")
public String boardWritePost(@ModelAttribute Board board) {
	User user = (User) session.getAttribute("user_info");
	String userId = user.getEmail();
	board.setUserId(userId);
	boardRepository.save(board);
	return "redirect:/board";
}
```

```java

```



### 3. RestTemplate: Open API 데이터 받기





