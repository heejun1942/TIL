# Spring 보조정리



## IoC / DI

>IoC(Inversion of Control)이란, 객체의 생성, 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀌었다는 것을 의미
>
>- 컴포넌트 의존관계 결정 설정 및 생명주기를 해결하기 위한 디자인 패턴



#### 1. IoC 컨테이너

- IoC 컨테이너는 객체의 생성을 책임지고, 의존성을 관리한다.
- POJO의 생성, 초기화, 서비스, 소멸에 대한 권한을 가진다.
- DL(Dependency Lookup)과 DI(Dependency Injection)로 분류되며, DL은 컨테이너의 종속성이 증가하여 주로 DI를 사용한다.



#### 2. DI

> **클래스간의 의존관계**를 빈 설정(Bean Definition) 정보를 바탕으로 **컨테이너가** 자동으로 **연결해주는 것**을 말함

- 객체 레퍼런스를 컨테이너로부터 주입 받아서, 실행 시 동적으로 의존관계가 생성된다.
- 컨테이너가 흐름의 주체가 되어 애플리케이션 코드에 의존관계를 주입해 주는 것이다.
- 장점: 코드가 단순해지며, 컨포넌트 간의 결합도가 제거된다.
- DI 유형
  - Setter Injection: 의존성을 입력 받는 setter 메서드를 만들고 이를 통해 의존성을 주입한다.
  - Constructor Injection: 필요한 의존성을 포함하는 클래스의 생성자를 만들고 이를 통해 의존성을 주입한다.



#### 3. Bean factory & Application Context

>Spring DI 컨테이너가 관리하는 객체를 빈(Bean)이라고 하고, 이 빈을 관리한다는 의미로 컨테이너를 빈 팩토리라고 부른다.

- Bean factory에 여러 가지 컨테이너 기능을 추가한 것을 **Application Context** (Application Context는 Bean factory를 상속받음)



## MVC (Model-View-Controller)

> MVC는 사용자 인터페이스로부터 비지니스 로직을 분리하여, 서로 영향 없이 쉽게 고칠 수 있는 애플리케이션을 만들 수 있게 해줌
>
> - Model: 애플리케이션의 정보 (데이터, Business Logic 포함)
> - View: 사용자에게 제공할 화면 (Presentation Logic)
> - Controller: Model과 View 사이의 상호 작용을 관리



<img src="https://user-images.githubusercontent.com/58925328/71407849-91615a80-267f-11ea-9768-d99c5700c194.PNG" width="80%" />



#### 1. Model 컴포넌트

- 데이터 저장소(ex. DB 등)와 연동하여 사용자가 입력한 데이터나 사용자에게 출력할 데이터를 다루는 일을 함

- DAO 클래스, Service 클래스에 해당



#### 2. View 컴포넌트

- 모델이 처리한 데이터나 그 작업 결과를 가지고 사용자에게 출력할 화면을 만드는 일을 함
- 생성된 화면은 웹 브라우저가 출력하고, 뷰 컴포넌트는 HTML과 CSS, Java Script를 사용하여 웹 브라우저가 출력할 UI를 만듦.



#### 3. Controller 컴포넌트

- 클라이언트의 요청을 받았을 때 그 요청에 대해 실제 업무를 수행하는 모델 컴포넌트를 호출하는 일을 함
- 클라이언트가 보낸 데이터가 있다면, 모델을 호출할 때 전달하기 쉽게 데이터를 적절히 가공하는 일을 함
- 모델이 업무 수행을 완료하면, 그 결과를 가지고 화면을 생성하도록 뷰에게 전달 (클라이언트 요청에 대해 모델과 뷰를 결정하여 전달)
- **Servlet**과 JSP를 사용하여 작성할 수 있음



<img src="https://user-images.githubusercontent.com/58925328/71411164-a643eb00-268b-11ea-844b-f5f2424a9fd3.PNG" width="80%" />





## RESTful 웹서비스

#### 1. Open API(Application Programming Interface)

>프로그래밍에서 사용할 수 있는 개방되어 있는 상태의 인터페이스를 말한다.
>
>대부분의 Open API는 REST 방식으로 지원된다.



#### 2. REST(REpresentational Safe Transfer)

>HTTP URI를 통해 제어할 자원을 명시하고, HTTP Method(GET, POST, PUT, DELETE)를 통해 해당 자원을 제어하는 명령을 내리는 방식의 아키텍쳐

- POST: Create/ GET: Read/ PUT: Update/ DELETE: Delete

- 기존방식:  `GET/list.do?no=510&name=java`  >  Querystring

  RESTful: `GET/bbs/java/510`



####  3. JSON

- Javascript에서 객체를 만들 때 사용하는 표현식을 의미
- XML을 대체하는 데이터 전송에 많이 사용된다.
- 특정 언어에 종속적이지 않음
- **Jackson**: JSON형태를 Java객체로, Java객체를 JSON형태로 변환해주는 Java 용 **JSON 라이브러리**