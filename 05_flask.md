# flask



### 1. flask 설치하기

```shell
 $ pip install flask==1.0.0 
```



- Flask 초기설정 코드

  (참고: https://www.palletsprojects.com/p/flask/)

```python
from flask import Flask, escape, request

app = Flask(__name__)

# cmd에서 'python hello.py'으로 실행하기 위해 추가시켜줘야함
if __name__==("__main__"):
    app.run(debug=True)
```



- Flask 기본 형식

  웹페이지에 "Hello, World" 출력하기

```python
from flask import Flask, escape, request

app = Flask(__name__)

#http://127.0.0.1:5000/
@app.route('/')
def hello():
    return "Hello, World"

if __name__==("__main__"):
    app.run(debug=True)
```



### 2. HTML로 출력하기

- python의 변수를 HTML파일로 보내서, HTML 페이지 출력하기.

- html파일은 flask 파이썬의 하위폴더 **/templates**을 만들어 하자.

  (주의: html이 있는 폴더명은 반드시 templates로 해야함)

  

`render_template('hi.html')`: html파일을 불러옴



[예제1] HTML파일에서 python변수를 사용하는 방법. `{{변수}}`

```python
# hello.py 파일
from flask import Flask, escape, request, render_template

app = Flask(__name__)

##http://127.0.0.1:5000/hi
@app.route('/hi')
def hi():
    name = "김희준"
    return render_template('hi.html', html_name = name)

if __name__=="__main__":
    app.run(debug=True)
```

```html
<!-- hi.html 파일 -->
<body>
    <h1>{{html_name}}</h1>
</body>
```



[예제2] 웹페이지 주소로 String변수를 받음

```python
# hello.py 파일
@app.route('/greeting/<string:name>/')
def greeting(name):
    def_name=name
    return render_template('greeting.html',html_name=def_name)
```

~~~html
<!-- hi.html 파일 -->
<body>
    <h1>만나서 반갑습니다. {{html_name}}님</h1>
</body>
~~~



[예제3] 웹페이지 주소로 Int변수를 받음

```python
# hello.py 파일
@app.route('/cube/<int:num>')
def cube(num):
    def_num = num
    def_cube = num**3
    return render_template('cube.html',html_num=def_num, html_cube=def_cube)
```

```html
<!-- hi.html 파일 -->
<body>
    <h2>{{html_num}}의 3제곱은</h2>
    <h2>{{html_cube}} 입니다.</h2>
</body>
```



### 3. 반복문/조건문 사용하기

> **html**파일에서 **python**문법 사용하기	

- {% %}으로 감싸줘야함

- 반복문, 조건문의 끝을 말해줘야함 

  - for문의 끝:`{% endfor %}` 
  
  - if문의 끝: `{% endif %}`



[예제4] 파이썬의 **list변수**를 받아, HTML에서 for문으로 출력

```python
@app.route('/movies')
def movies():
    movies= ['조커','겨울왕국2','터미네이터','어벤져스']
    return render_template('movie.html', movies=movies)
```

```html
<body>
    {% for movie in movies %}
        <li>{{ movie }}</li>
    {% endfor %}
</body>
```



[예제5] `.py`에서 `.html`로 리스트 변수를 받아서 if문과 for문 사용하기

```python
@app.route('/movies')
def movies():
    movies= ['조커','겨울왕국2','터미네이터','어벤져스']
    return render_template('movie.html', movies=movies)
```

````html
<body>
    {% for movie in movies %}
        {% if movie =='조커' %}
            <li>{{movie}} (이 영화 진짜 재밌어!)</li>
        {% elif movie == '겨울왕국2' %}
            <li>{{movie}} (역시 겨울왕국!)</li>
        {% else %}
            <li>{{movie}}</li>
        {% endif %}
    {% endfor %}
</body>
````



### 4. form태그로 값 보내기

> - ruquest.args.get("[변수]"): 페이지로 보낸 변수를 받음



[예제]  *ping*페이지에서 *pong*페이지로 값 보내기

1. *ping* 에서 form태그로 keyword 값을 받음
2. *pong*페이지로 keyword값 전송.  `.py`가 받음
3. `.py`에서 keyword변수의 값을 data변수에 넣고, data를 *pong*으로 보냄

```python
#ping_pong.py 파일

@app.route('/ping')
def ping():
    return render_template('ping.html')

@app.route('/pong')
def pong():
    data=request.args.get("keyword")
    return render_template('pong.html', data = data)
```

```html
<!-- ping.html 파일 -->

<body>
    <h1>Here is Ping!!</h1>
    <form action="/pong">
        <input type="text" name="keyword">
        <input type="submit">
    </form>
</body>
```

```html
<!-- pong.html 파일 -->

<body>
    <h1>여기는 Pong 입니다!</h1>
    {{data}}
</body>
```



### 4. 웹 크롤링을 통해 값 받기

*search*페이지에서 유저를 검색하면 `op_gg.py`에서 웹 크롤링하여 유저정보를 *opgg* 페이지로 전송

1. *search*에서 form태그를 통해 유저이름을 받아 `op_gg.py`로 전송
2. `op_gg.py`에서 유저이름을 받음 > op.gg사이트의 해당 유저정보를 크롤링.
3. 유저정보를 *opgg*페이지로 전송

op.gg페이지에서 

```python
#op_gg.py

from flask import Flask, escape, request, render_template
from bs4 import BeautifulSoup
import requests


app = Flask(__name__)

@app.route('/search')
def search():
    return render_template('search.html')

@app.route('/opgg')
def opgg():
    userName = request.args.get('userName')
    
    url = f"https://www.op.gg/summoner/userName={userName}"
    req = requests.get(url).text
    
    data= BeautifulSoup(req, 'html.parser')
    tier=data.select_one("#SummonerLayoutContent > div.tabItem.Content.SummonerLayoutContent.summonerLayout-summary > div.SideContent > div.TierBox.Box > div > div.TierRankInfo > div.TierRank")
    win=data.select_one("#SummonerLayoutContent > div.tabItem.Content.SummonerLayoutContent.summonerLayout-summary > div.SideContent > div.TierBox.Box > div > div.TierRankInfo > div.TierInfo > span.WinLose > span.wins")
    
    tier=tier.text
    win=win.text[:-1]

    return render_template('opgg.html', userName=userName, tier=tier,win=win)

if __name__==("__main__"):
    app.run(debug=True)
    
```

```html
<!-- search.html 파일 -->

<body>
    <form action="/opgg">
        <input type="text" name="userName">
        <input type="submit" value="검색">
    </form>
</body>
```



```html
<!-- opgg.html 파일 -->

<body>
    <h1>{{userName}} 님의 링크는</h1>
    <h2>{{tier}} 입니다.</h2>
    <h3>{{win}} 승 하셨습니다.</h3>
</body>
```



