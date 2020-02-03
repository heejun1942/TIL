## Django (장고)

`conda install django`: 장고 다운

플라스크...? 비교..

`python manage.py runserver`: 서버 실행







### 1. 구조

> 장고도 **MVC 방식**임 > MTV패턴으로 부름.
>
> model, template, view로 각각 MVC의 model, view, controller 역할을 함. 

- model.py, template.py, view.py 모두 앱 디렉토리에 존재.

- STS의 Controller역할: views.py, urls.py

  - 앱 > views.py : 요청을 받아, 모델을 실행한 후 응답. 함수나 클래스로 작성.

  - 프로젝트 > urls.py : url과 views의 함수를 routing

    ※ 참고: 앱별로 url을 관리하기 위해 앱 디렉토리에 urls.py을 생성한 후 연결해줌.

- models.py
  - 장고의 내장 ORM(object relation model)로 SQL을 직접 작성하지 않아도 model을 통해 **DB에 접근**
  - 이러한 model의 클래스를 views.py에서 import하여 사용.



### 1-1. views.py

model에서 데이터를 가져온 후 templates의 html로 정보를 전달. 

```python
from .models import Curriculum

def show(request):
    # curriculum 테이블의 인스턴스 전부 가져오기.
    curriculum = Curriculum.objects.all()
    # 디렉토리 형태로 데이터 보냄.
    return render(request, 'firstapp/show.html', {'list':curriculum})
```





### 1-2. models.py

>파이썬의 클래스와 DB의 테이블을 매핑

- model의 두가지 역할
  - 생성: migration코드 이용

  - 관리

 `python manage.py makemigrations [app이름]`:  app의 모델 변경사항 확인

` python manage.py migrate `: 변경사항을 데이터베이스로 반영



### 1-3. templates

앱 디렉토리에 templates디렉토리 생성. (앱/templates/앱명 디렉토리/*.html)

```python
<body>
# html에서 python문법을 사용할때는 {% %}을 사용
# 변수는 {{ }}를 사용

    {% for item in list %}
        <h3>{{item.id}} : {{item.name}}</h3>
    {% endfor %}
</body>
```



### 2. 관리자 기능

관리자 페이지: http://localhost:8000/admin

`python manage.py createsuperuser`: 관리자 생성

▼ 관리자 페이지에서 데이터 제어를 위한 세팅

```python
# 앱 > admin.py
from django.contrib import admin
from .models import Curriculum

# 데이터를 관리자 페이지에서 제어할 수 있게 등록
admin.site.register(Curriculum)
```



### 3. setting.py

- INSTALLED_APPS: 프로젝트에 생성한 App을 추가
- DATABASES: 데이터베이스 설정 (mariaDB의 연결할 DB를 여기에 설정해줌.)

`conda install mysqlclient`: mysqlclient 설치

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'django',
        'USER': 'root',
        'PASSWORD': '1234',
        'HOST': 'localhost',
        'PORT': 3306
    }
}
```





## 장고 튜토리얼 투표앱



데이터베이스 관련 API 테스트

 `python manage.py shell`: 장고 shell 접속. 쉘을 통해 데이터 확인



\__init__   인스턴스 생성시 자동으로 실행되는 함수

\__str__   인스턴스자체를 출력할 때 형식을 지정하는 함수



url로 변수받기 (마치 STS의 @Pathvariable)

```python
# polls/urls.py

urlpatterns = [
 path('', views.index, name='index'),
 path('<int:question_id>/', views.detail, name='detail'),
 path('<int:question_id>/results/', views.results, name='results'),
 path('<int:question_id>/vote/', views.vote, name='vote'),

]
```

url을 통해 question_id의 값을 views에서 받음.

```python
# polls/views.py

# question_id는 url을 통해 받는다.
def detail(request, question_id):
    question= Question.objects.get(pk=question_id)
    return render(request, 'polls/detail.html', {'question': question})
```

Question 모델의 데이터만 받았지만 fk로 연결된 Choice모델의 데이터를 사용할 수 있음.

```python
# templates/polls/detail.html

<u1>
# Question모델로 Choice테이블의 데이터를 불러옴.
{% for choice in question.choice_set.all %}
    <li>{{choice.choice_text}}</li>
{% endfor %}
</u1>
```





{{변수명}}

html에서 전달받은 데이터를 사용할 때

html에서 파이썬 문법 안에서도 가능

